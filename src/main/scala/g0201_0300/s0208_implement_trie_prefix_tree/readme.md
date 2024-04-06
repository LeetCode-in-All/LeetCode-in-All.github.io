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

```scala
class Trie() {
    private val root = new TrieNode
    private var startsWith = false

    private class TrieNode {
        val children = new Array[TrieNode](26)
        var isWord = false
    }

    def insert(word: String): Unit = {
        insert(word, root, 0)
    }

    private def insert(word: String, current: TrieNode, index: Int): Unit = {
        if (index == word.length) {
            current.isWord = true
            return
        }
        val charIndex = word.charAt(index) - 'a'
        if (current.children(charIndex) == null) {
            current.children(charIndex) = new TrieNode
        }
        insert(word, current.children(charIndex), index + 1)
    }

    def search(word: String): Boolean = {
        search(word, root, 0)
    }

    private def search(word: String, current: TrieNode, index: Int): Boolean = {
        if (index == word.length) {
            startsWith = true
            current.isWord
        } else {
            val charIndex = word.charAt(index) - 'a'
            if (current.children(charIndex) == null) {
                startsWith = false
                false
            } else {
                search(word, current.children(charIndex), index + 1)
            }
        }
    }

    def startsWith(prefix: String): Boolean = {
        search(prefix)
        startsWith
    }
}
```