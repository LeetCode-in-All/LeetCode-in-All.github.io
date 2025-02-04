[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 45\. Jump Game II

Medium

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

**Example 1:**

**Input:** nums = [2,3,1,1,4]

**Output:** 2

**Explanation:** The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

**Input:** nums = [2,3,0,1,4]

**Output:** 2

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   `0 <= nums[i] <= 1000`

## Solution

```racket
(define (init-vec len)
  (let ([prepare-vec (make-vector len 99999)])
    (begin (vector-set! prepare-vec 0 0) prepare-vec)))

(define (set-cost! vec p elem)
  (if (= elem 0) vec
      (let* ([p-cost (vector-ref vec p)]
             [now-cost (add1 p-cost)]
             [target-cost (vector-ref vec (+ p elem))])
        (begin (vector-set! vec (+ p elem) (min now-cost target-cost))
               (set-cost! vec p (- elem 1))))))

(define (simple-dp cache p steps)
  (if (= 0 (length steps)) (vector-ref cache (- p 1))
      (simple-dp (set-cost! cache p (car steps)) (add1 p) (cdr steps))))

(define (start-dp steps) (simple-dp (init-vec 200000) 0 steps))

(define/contract (jump nums)
  (-> (listof exact-integer?) exact-integer?)
  (start-dp nums))
```