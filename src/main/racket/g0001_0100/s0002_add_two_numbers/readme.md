[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 2\. Add Two Numbers

Medium

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

**Input:** l1 = [2,4,3], l2 = [5,6,4]

**Output:** [7,0,8]

**Explanation:** 342 + 465 = 807. 

**Example 2:**

**Input:** l1 = [0], l2 = [0]

**Output:** [0] 

**Example 3:**

**Input:** l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]

**Output:** [8,9,9,9,0,0,0,1] 

**Constraints:**

*   The number of nodes in each linked list is in the range `[1, 100]`.
*   `0 <= Node.val <= 9`
*   It is guaranteed that the list represents a number that does not have leading zeros.

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

(define/contract (add-two-numbers l1 l2)
  (-> (or/c list-node? #f) (or/c list-node? #f) (or/c list-node? #f))
  (add-two-numbers-help l1 l2 0)
  )

(define (add-two-numbers-help l1 l2 carry-sum)
    (cond
        [(and (false? l1) (false? l2)) (if (zero? carry-sum) #f (list-node carry-sum #f))]
        [(false? l1) (list-node (modulo (+ (list-node-val l2) carry-sum) 10) (add-two-numbers-help l1 (list-node-next l2) (/ (- (+ (list-node-val l2) carry-sum) (modulo (+ (list-node-val l2) carry-sum) 10)) 10)))]
        [(false? l2) (list-node (modulo (+ (list-node-val l1) carry-sum) 10) (add-two-numbers-help (list-node-next l1) l2 (/ (- (+ (list-node-val l1) carry-sum) (modulo (+ (list-node-val l1) carry-sum) 10)) 10)))]
        [else (list-node (modulo (+ (list-node-val l1) (list-node-val l2) carry-sum) 10) (add-two-numbers-help (list-node-next l1) (list-node-next l2) (/ (- (+ (list-node-val l1) (list-node-val l2) carry-sum) (modulo (+ (list-node-val l1) (list-node-val l2) carry-sum) 10)) 10)))]
    )
)
```