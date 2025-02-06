[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 114\. Flatten Binary Tree to Linked List

Medium

Given the `root` of a binary tree, flatten the tree into a "linked list":

*   The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
*   The "linked list" should be in the same order as a [**pre-order** **traversal**](https://en.wikipedia.org/wiki/Tree_traversal#Pre-order,_NLR) of the binary tree.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg)

**Input:** root = [1,2,5,3,4,null,6]

**Output:** [1,null,2,null,3,null,4,null,5,null,6]

**Example 2:**

**Input:** root = []

**Output:** []

**Example 3:**

**Input:** root = [0]

**Output:** [0]

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 2000]`.
*   `-100 <= Node.val <= 100`

**Follow up:** Can you flatten the tree in-place (with `O(1)` extra space)?

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

(define/contract (flatten root)
  (-> (or/c tree-node? #f) void?)
  
  (define (find-tail root)
    (cond
      [(not root) root]
      [else
       (let ([left (tree-node-left root)]
             [right (tree-node-right root)])
         (if left
             (let ([tail (find-tail left)])
               ; Stitch right subtree below the tail
               (set-tree-node-left! root #f)
               (set-tree-node-right! root left)
               (when tail
                 (set-tree-node-right! tail right))
               ; Return final tail
               (if (and tail (tree-node-right tail))
                   (find-tail (tree-node-right tail))
                   tail))
             ; If no left subtree, current node is tail
             (if (tree-node-right root)
                 (find-tail (tree-node-right root))
                 root)))]))
  
  (when root
    (find-tail root))
  (void))
```