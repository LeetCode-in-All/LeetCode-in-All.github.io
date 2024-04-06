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

```php
class TrieNode {
    public $children;
    public $isWord;

    function __construct() {
        $this->children = array_fill(0, 26, null);
        $this->isWord = false;
    }
}

class Trie {
    private $root;
    private $startWith;

    function __construct() {
        $this->root = new TrieNode();
        $this->startWith = false;
    }

    /**
     * @param String $word
     * @return NULL
     */
    public function insert($word) {
        $this->insertInternal($word, $this->root, 0);
    }

    private function insertInternal($word, $root, $idx) {
        if ($idx == strlen($word)) {
            $root->isWord = true;
            return;
        }
        $index = ord($word[$idx]) - ord('a');
        if ($root->children[$index] == null) {
            $root->children[$index] = new TrieNode();
        }
        $this->insertInternal($word, $root->children[$index], $idx + 1);
    }

    /**
     * @param String $word
     * @return Boolean
     */
    public function search($word) {
        return $this->searchInternal($word, $this->root, 0);
    }

    private function searchInternal($word, $root, $idx) {
        if ($idx == strlen($word)) {
            $this->startWith = true;
            return $root->isWord;
        }
        $index = ord($word[$idx]) - ord('a');
        if ($root->children[$index] == null) {
            $this->startWith = false;
            return false;
        }
        return $this->searchInternal($word, $root->children[$index], $idx + 1);
    }

    /**
     * @param String $prefix
     * @return Boolean
     */
    public function startsWith($prefix) {
        $this->search($prefix);
        return $this->startWith;
    }
}
/**
 * Your Trie object will be instantiated and called as such:
 * $obj = Trie();
 * $obj->insert($word);
 * $ret_2 = $obj->search($word);
 * $ret_3 = $obj->startsWith($prefix);
 */
```