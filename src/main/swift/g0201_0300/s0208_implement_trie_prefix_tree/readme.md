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

```swift
final class TrieNode {
    let data: Character
    var children: [TrieNode] = []
    var endOfWord: Bool = false
    init(_ data: Character) {
        self.data = data
    }
}

class Trie {
    var trie: TrieNode
    init() {
        trie = TrieNode(" ")
    }
    // add the first letter to this class's children
    // recursively, create new node to the next child and move to the next index
    // once we hit the end of the word, set the TrieNode.endOfWord = true
    func insert(_ word: String) {
        var wordArray = Array(word)
        var startNode = trie
        self.insert(&wordArray, 0, startNode)
    }

    private func insert(_ word: inout [Character], _ index: Int, _ node: TrieNode?) {
        guard let node else { return }
        guard index < word.count else {
            node.endOfWord = true
            return
        }
        var currNode: TrieNode?
        for childNode in node.children {
            if childNode.data == word[index] {
                currNode = childNode
                break
            }
        }
        if currNode == nil {
            currNode = TrieNode(word[index])
            node.children.append(currNode!)
        }
        let index = index + 1
        self.insert(&word, index, currNode)
    }
    
    func search(_ word: String) -> Bool {
        var words = Array(word)
        var trie = self.trie
        for letter in words {
            var foundLetter = false
            for child in trie.children {
                if letter == child.data {
                    trie = child
                    foundLetter = true
                    break
                }
            }
            if foundLetter == false {
                return false
            }
        }
        return trie.endOfWord
    }
    
    func startsWith(_ prefix: String) -> Bool {
        var words = Array(prefix)
        var trie = self.trie
        for letter in words {
            var foundLetter = false
            for child in trie.children {
                if letter == child.data {
                    trie = child
                    foundLetter = true
                    break
                }
            }
            if foundLetter == false {
                return false
            }
        }
        return true
    }
}

/*
 * Your Trie object will be instantiated and called as such:
 * let obj = Trie()
 * obj.insert(word)
 * let ret_2: Bool = obj.search(word)
 * let ret_3: Bool = obj.startsWith(prefix)
 */
```