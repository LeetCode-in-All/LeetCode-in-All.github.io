[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 208\. Implement Trie (Prefix Tree)

Medium

A [**trie**](https://en.wikipedia.org/wiki/Trie) (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

*   `Trie()` Initializes the trie object.
*   `void insert(String word)` Inserts the string `word` into the trie.
*   `boolean search(String word)` Returns `true` if the string `word` is in the trie (i.e., was inserted before), and `false` otherwise.
*   `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string `word` that has the prefix `prefix`, and `false` otherwise.

**Example 1:**

**Input** ["Trie", "insert", "search", "search", "startsWith", "insert", "search"] [[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]

**Output:** [null, null, true, false, true, null, true]

**Explanation:** 

Trie trie = new Trie(); 

trie.insert("apple"); 

trie.search("apple"); // return True 

trie.search("app"); // return False 

trie.startsWith("app"); // return True 

trie.insert("app"); 

trie.search("app"); // return True

**Constraints:**

*   `1 <= word.length, prefix.length <= 2000`
*   `word` and `prefix` consist only of lowercase English letters.
*   At most <code>3 * 10<sup>4</sup></code> calls **in total** will be made to `insert`, `search`, and `startsWith`.

## Solution

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <string.h>

#define ALPHABET_SIZE 26

typedef struct TrieNode {
    struct TrieNode* children[ALPHABET_SIZE];
    bool isWord;
} TrieNode;

typedef struct Trie {
    TrieNode* root;
} Trie;

// Helper function to create a new TrieNode
TrieNode* createTrieNode() {
    TrieNode* node = (TrieNode*)malloc(sizeof(TrieNode));
    for (int i = 0; i < ALPHABET_SIZE; i++) {
        node->children[i] = NULL;
    }
    node->isWord = false;
    return node;
}

// Function to create a new Trie
Trie* trieCreate() {
    Trie* trie = (Trie*)malloc(sizeof(Trie));
    trie->root = createTrieNode();
    return trie;
}

// Function to insert a word into the Trie
void trieInsert(Trie* obj, char* word) {
    TrieNode* node = obj->root;
    for (int i = 0; i < strlen(word); i++) {
        int index = word[i] - 'a';
        if (node->children[index] == NULL) {
            node->children[index] = createTrieNode();
        }
        node = node->children[index];
    }
    node->isWord = true;
}

// Recursive helper function to search for a word or prefix
bool trieSearchHelper(TrieNode* node, char* word, bool checkPrefix) {
    for (int i = 0; i < strlen(word); i++) {
        int index = word[i] - 'a';
        if (node->children[index] == NULL) {
            return false;
        }
        node = node->children[index];
    }
    return checkPrefix || node->isWord;
}

// Function to search for a complete word in the Trie
bool trieSearch(Trie* obj, char* word) {
    return trieSearchHelper(obj->root, word, false);
}

// Function to check if any word in the Trie starts with the given prefix
bool trieStartsWith(Trie* obj, char* prefix) {
    return trieSearchHelper(obj->root, prefix, true);
}

// Recursive function to free all TrieNodes
void trieFreeNode(TrieNode* node) {
    if (node == NULL) return;
    for (int i = 0; i < ALPHABET_SIZE; i++) {
        trieFreeNode(node->children[i]);
    }
    free(node);
}

// Function to free the entire Trie
void trieFree(Trie* obj) {
    trieFreeNode(obj->root);
    free(obj);
}

/**
 * Your Trie struct will be instantiated and called as such:
 * Trie* obj = trieCreate();
 * trieInsert(obj, word);
 
 * bool param_2 = trieSearch(obj, word);
 
 * bool param_3 = trieStartsWith(obj, prefix);
 
 * trieFree(obj);
*/
```