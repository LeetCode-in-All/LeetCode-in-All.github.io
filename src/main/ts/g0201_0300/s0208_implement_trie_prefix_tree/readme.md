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

```typescript
class TrieNode {
    children: TrieNode[]
    isWord: boolean

    constructor() {
        this.children = new Array<TrieNode>(26)
        this.isWord = false
    }
}

class Trie {
    private root: TrieNode
    private startWith: boolean

    private static readonly ALPHABET_SIZE = 26

    constructor() {
        this.root = new TrieNode()
        this.startWith = false
    }

    // Inserts a word into the trie.
    insert(word: string): void {
        this.insertRecursive(word, this.root, 0)
    }

    private insertRecursive(word: string, node: TrieNode, idx: number): void {
        if (idx === word.length) {
            node.isWord = true
            return
        }
        const charIndex = this.getCharIndex(word.charAt(idx))
        if (!node.children[charIndex]) {
            node.children[charIndex] = new TrieNode()
        }
        this.insertRecursive(word, node.children[charIndex], idx + 1)
    }

    // Returns if the word is in the trie.
    search(word: string): boolean {
        this.startWith = false
        return this.searchRecursive(word, this.root, 0)
    }

    private searchRecursive(word: string, node: TrieNode, idx: number): boolean {
        if (idx === word.length) {
            this.startWith = true
            return node.isWord
        }

        const charIndex = this.getCharIndex(word.charAt(idx))
        if (!node.children[charIndex]) {
            this.startWith = false
            return false
        }
        return this.searchRecursive(word, node.children[charIndex], idx + 1)
    }

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    startsWith(prefix: string): boolean {
        this.search(prefix)
        return this.startWith
    }

    private getCharIndex(char: string): number {
        return char.charCodeAt(0) - 'a'.charCodeAt(0)
    }
}

/*
 * Your Trie object will be instantiated and called as such:
 * var obj = new Trie()
 * obj.insert(word)
 * var param_2 = obj.search(word)
 * var param_3 = obj.startsWith(prefix)
 */

export { Trie }
```