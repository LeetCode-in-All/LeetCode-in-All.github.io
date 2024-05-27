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

**Input**

    ["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
    [[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]

**Output:** [null, null, true, false, true, null, true]

**Explanation:**

    Trie trie = new Trie();
    trie.insert("apple"); trie.search("apple"); // return True
    trie.search("app"); // return False
    trie.startsWith("app"); // return True
    trie.insert("app");
    trie.search("app"); // return True 

**Constraints:**

*   `1 <= word.length, prefix.length <= 2000`
*   `word` and `prefix` consist only of lowercase English letters.
*   At most <code>3 * 10<sup>4</sup></code> calls **in total** will be made to `insert`, `search`, and `startsWith`.

## Solution

```cpp
#include <string>
#include <vector>

class Trie {
private:
    struct TrieNode {
        std::vector<TrieNode*> children;
        bool isWord;

        TrieNode() : children(26, nullptr), isWord(false) {}
    };

    TrieNode* root;
    bool startWith;

    void insert(const std::string& word, TrieNode* node, int idx) {
        if (idx == word.length()) {
            node->isWord = true;
            return;
        }
        int index = word[idx] - 'a';
        if (node->children[index] == nullptr) {
            node->children[index] = new TrieNode();
        }
        insert(word, node->children[index], idx + 1);
    }

    bool search(const std::string& word, TrieNode* node, int idx) {
        if (idx == word.length()) {
            startWith = true;
            return node->isWord;
        }
        int index = word[idx] - 'a';
        if (node->children[index] == nullptr) {
            startWith = false;
            return false;
        }
        return search(word, node->children[index], idx + 1);
    }

public:
    Trie() : root(new TrieNode()), startWith(false) {}

    void insert(const std::string& word) {
        insert(word, root, 0);
    }

    bool search(const std::string& word) {
        return search(word, root, 0);
    }

    bool startsWith(const std::string& prefix) {
        search(prefix, root, 0);
        return startWith;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```