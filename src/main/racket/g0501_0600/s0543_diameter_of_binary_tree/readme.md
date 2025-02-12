[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 543\. Diameter of Binary Tree

Easy

Given the `root` of a binary tree, return _the length of the **diameter** of the tree_.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)

**Input:** root = [1,2,3,4,5]

**Output:** 3

**Explanation:** 3 is the length of the path [4,2,1,3] or [5,2,1,3].

**Example 2:**

**Input:** root = [1,2]

**Output:** 1

**Constraints:**

*   The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.
*   `-100 <= Node.val <= 100`

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

(define/contract (diameter-of-binary-tree root)
  (-> (or/c tree-node? #f) exact-integer?)
  ; Use let/cc to simulate a mutable variable for diameter
  (let/cc return
    (let ([diameter 0])
      ; Helper function that both updates max diameter and returns height
      (define (diameter-helper node)
        (if (not node)
            0
            (let* ([left-len (if (tree-node-left node)
                                (add1 (diameter-helper (tree-node-left node)))
                                0)]
                   [right-len (if (tree-node-right node)
                                 (add1 (diameter-helper (tree-node-right node)))
                                 0)])
              ; Update diameter if current path is longer
              (set! diameter (max diameter (+ left-len right-len)))
              ; Return max height of this subtree
              (max left-len right-len))))
      
      ; Call helper function and return final diameter
      (diameter-helper root)
      diameter)))
```