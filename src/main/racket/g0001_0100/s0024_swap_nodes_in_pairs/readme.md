[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 24\. Swap Nodes in Pairs

Medium

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)

**Input:** head = [1,2,3,4]

**Output:** [2,1,4,3]

**Example 2:**

**Input:** head = []

**Output:** []

**Example 3:**

**Input:** head = [1]

**Output:** [1]

**Constraints:**

*   The number of nodes in the list is in the range `[0, 100]`.
*   `0 <= Node.val <= 100`

## Solution

```racket
; Definition for singly-linked list:
#|

; val : integer?
; next : (or/c list-node? #f)
(struct list-node
  (val next) #:mutable #:transparent)

; constructor
(define (make-list-node [val 0])
  (list-node val #f))

|#

(define (swap-pairs head)
  (let ([dummy (list-node 0 head)])
    (begin
        (set-list-node-next! dummy head)
        (let loop ([cur head]        
                  [prev dummy])
          (cond 
                [(or (eq? cur #f) (eq? (list-node-next cur) #f)) #f]
                [else (begin
                   (set-list-node-next! prev (list-node-next cur))
                   (set-list-node-next! cur (list-node-next (list-node-next cur)))
                   (set-list-node-next! (list-node-next prev) cur)

                   (loop (list-node-next cur) cur))]))
        (list-node-next dummy))))
```