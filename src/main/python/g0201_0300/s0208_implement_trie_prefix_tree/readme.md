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

```python
class TrieNode:
    # Initialize your data structure here.
    def __init__(self):
        self.children = [None] * 26
        self.isWord = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
        self.startWith = False

    # Inserts a word into the trie.
    def insert(self, word):
        self._insert(word, self.root, 0)

    def _insert(self, word, root, idx):
        if idx == len(word):
            root.isWord = True
            return
        index = ord(word[idx]) - ord('a')
        if root.children[index] is None:
            root.children[index] = TrieNode()
        self._insert(word, root.children[index], idx + 1)

    # Returns if the word is in the trie.
    def search(self, word):
        return self._search(word, self.root, 0)

    def _search(self, word, root, idx):
        if idx == len(word):
            self.startWith = True
            return root.isWord
        index = ord(word[idx]) - ord('a')
        if root.children[index] is None:
            self.startWith = False
            return False
        return self._search(word, root.children[index], idx + 1)

    # Returns if there is any word in the trie
    # that starts with the given prefix.
    def startsWith(self, prefix):
        self.search(prefix)
        return self.startWith

# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```