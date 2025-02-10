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

```racket
(define trie%
  (class object%
    (super-new)

    ;; Define TrieNode struct
    (struct trie-node (children is-word?) #:mutable)

    ;; Root node of the Trie
    (init-field)
    (define root (trie-node (make-hash) #f))
    (define start-with? #f)

    ;; Inserts a word into the trie.
    (define/public (insert word)
      (define (insert-helper node word idx)
        (if (= idx (string-length word))
            (set-trie-node-is-word?! node #t)
            (let* ([ch (string-ref word idx)]
                   [children (trie-node-children node)]
                   [next-node (hash-ref children ch (lambda () (trie-node (make-hash) #f)))])
              (hash-set! children ch next-node)
              (insert-helper next-node word (+ idx 1)))))
      (insert-helper root word 0))

    ;; Searches for a word in the trie.
    (define/public (search word)
      (define (search-helper node word idx)
        (if (= idx (string-length word))
            (begin
              (set! start-with? #t)
              (trie-node-is-word? node))
            (let* ([ch (string-ref word idx)]
                   [children (trie-node-children node)]
                   [next-node (hash-ref children ch #f)])
              (if next-node
                  (search-helper next-node word (+ idx 1))
                  (begin
                    (set! start-with? #f)
                    #f)))))
      (search-helper root word 0))

    ;; Checks if any word in the trie starts with the given prefix.
    (define/public (starts-with prefix)
      (send this search prefix)
      start-with?)))

;; Your trie% object will be instantiated and called as such:
;; (define obj (new trie%))
;; (send obj insert word)
;; (define param_2 (send obj search word))
;; (define param_3 (send obj starts-with prefix))
```