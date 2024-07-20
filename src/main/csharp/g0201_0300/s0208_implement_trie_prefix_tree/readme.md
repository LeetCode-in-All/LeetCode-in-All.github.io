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

```csharp
public class Trie {
    private TrieNode root;
    private bool startWith;

    private class TrieNode {
        // Initialize your data structure here.
        public TrieNode[] children;
        public bool isWord;

        public TrieNode() {
            children = new TrieNode[26];
        }
    }

    public Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    public void Insert(string word) {
        Insert(word, root, 0);
    }

    private void Insert(string word, TrieNode root, int idx) {
        if (idx == word.Length) {
            root.isWord = true;
            return;
        }
        int index = word[idx] - 'a';
        if (root.children[index] == null) {
            root.children[index] = new TrieNode();
        }
        Insert(word, root.children[index], idx + 1);
    }

    // Returns if the word is in the trie.
    public bool Search(string word) {
        return Search(word, root, 0);
    }

    private bool Search(string word, TrieNode root, int idx) {
        if (idx == word.Length) {
            startWith = true;
            return root.isWord;
        }
        int index = word[idx] - 'a';
        if (root.children[index] == null) {
            startWith = false;
            return false;
        }
        return Search(word, root.children[index], idx + 1);
    }

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public bool StartsWith(string prefix) {
        Search(prefix);
        return startWith;
    }
}
/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.Insert(word);
 * bool param_2 = obj.Search(word);
 * bool param_3 = obj.StartsWith(prefix);
}
```