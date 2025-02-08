[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 148\. Sort List

Medium

Given the `head` of a linked list, return _the list after sorting it in **ascending order**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg)

**Input:** head = [4,2,1,3]

**Output:** [1,2,3,4]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg)

**Input:** head = [-1,5,3,4,0]

**Output:** [-1,0,3,4,5]

**Example 3:**

**Input:** head = []

**Output:** []

**Constraints:**

*   The number of nodes in the list is in the range <code>[0, 5 * 10<sup>4</sup>]</code>.
*   <code>-10<sup>5</sup> <= Node.val <= 10<sup>5</sup></code>

**Follow up:** Can you sort the linked list in `O(n logn)` time and `O(1)` memory (i.e. constant space)?

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

; Helper function to split the list into two halves
(define (split-list head)
  (let loop ([slow head]
             [fast head]
             [pre #f])
    (cond
      [(or (not fast) (not (list-node-next fast)))
       (when pre
         (set-list-node-next! pre #f))
       slow]
      [else
       (loop (list-node-next slow)
             (list-node-next (list-node-next fast))
             slow)])))

; Helper function to merge two sorted lists
(define (merge-lists l1 l2)
  (let ([dummy (list-node 1 #f)])
    (let loop ([curr dummy]
               [first l1]
               [second l2])
      (cond
        [(not first)
         (set-list-node-next! curr second)]
        [(not second)
         (set-list-node-next! curr first)]
        [else
         (if (<= (list-node-val first) (list-node-val second))
             (begin
               (set-list-node-next! curr first)
               (loop first (list-node-next first) second))
             (begin
               (set-list-node-next! curr second)
               (loop second first (list-node-next second))))])
      (list-node-next dummy))))

; Main sort-list function with contract
(define/contract (sort-list head)
  (-> (or/c list-node? #f) (or/c list-node? #f))
  (cond
    [(or (not head) (not (list-node-next head)))
     head]
    [else
     (let* ([middle (split-list head)]
            [first (sort-list head)]
            [second (sort-list middle)])
       (merge-lists first second))]))
```