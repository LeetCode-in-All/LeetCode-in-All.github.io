[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 105\. Construct Binary Tree from Preorder and Inorder Traversal

Medium

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return _the binary tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

**Input:** preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]

**Output:** [3,9,20,null,null,15,7]

**Example 2:**

**Input:** preorder = [-1], inorder = [-1]

**Output:** [-1]

**Constraints:**

*   `1 <= preorder.length <= 3000`
*   `inorder.length == preorder.length`
*   `-3000 <= preorder[i], inorder[i] <= 3000`
*   `preorder` and `inorder` consist of **unique** values.
*   Each value of `inorder` also appears in `preorder`.
*   `preorder` is **guaranteed** to be the preorder traversal of the tree.
*   `inorder` is **guaranteed** to be the inorder traversal of the tree.

## Solution

```racket
; Definition for a binary tree node.
#|

; val : integer?
; left : (or/c tree-node? #f)
; right : (or/c tree-node? #f)
(struct tree-node
  (val left right) #:mutable #:transparent)

; constructor
(define (make-tree-node [val 0])
  (tree-node val #f #f))

|#

(define/contract (build-tree preorder inorder)
  (-> (listof exact-integer?) (listof exact-integer?) (or/c tree-node? #f))
  
  ; Create a hash table mapping values to their indices in inorder traversal
  (define inorder-map
    (for/hash ([val inorder]
               [idx (range (length inorder))])
      (values val idx)))
  
  ; Helper function that builds the tree recursively
  (define (build j start end)
    (if (or (> start end) 
            (>= j (length preorder)))
        #f
        (let* ([value (list-ref preorder j)]
               [index (hash-ref inorder-map value)]
               [node (tree-node value #f #f)]
               [left-subtree (build (add1 j) start (sub1 index))]
               [right-subtree (build (+ j 1 (- index start)) (add1 index) end)])
          (struct-copy tree-node node
                      [left left-subtree]
                      [right right-subtree]))))
  
  ; Start the tree building process
  (if (empty? preorder)
      #f
      (build 0 0 (sub1 (length preorder)))))
```