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

```golang
import "strings"

type node struct {
	val   string
	left  *node
	right *node
}

type Trie struct {
	root *node
}

func Constructor() Trie {
	return Trie{}
}

func (t *Trie) Insert(word string) {
	t.root = insert(t.root, word)
}

func (t *Trie) Search(word string) bool {
	return search(t.root, word)
}

func (t *Trie) StartsWith(prefix string) bool {
	return startsWith(t.root, prefix)
}

func startsWith(root *node, prefix string) bool {
	if root == nil {
		return false
	}
	if strings.Index(root.val, prefix) == 0 {
		return true
	}
	if prefix < root.val {
		return startsWith(root.left, prefix)
	}
	return startsWith(root.right, prefix)
}

func search(root *node, word string) bool {
	if root == nil {
		return false
	}
	if word == root.val {
		return true
	}
	if word < root.val {
		return search(root.left, word)
	}
	return search(root.right, word)
}

func insert(root *node, word string) *node {
	if root == nil {
		return &node{word, nil, nil}
	}
	if word == root.val {
		return root
	}
	if word < root.val {
		root.left = insert(root.left, word)
	} else {
		root.right = insert(root.right, word)
	}
	return root
}

/**
 * Your Trie object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Insert(word);
 * param_2 := obj.Search(word);
 * param_3 := obj.StartsWith(prefix);
 */
```