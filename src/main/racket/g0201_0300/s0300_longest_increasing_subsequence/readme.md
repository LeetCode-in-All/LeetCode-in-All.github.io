[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 300\. Longest Increasing Subsequence

Medium

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, `[3,6,2,7]` is a subsequence of the array `[0,3,1,6,2,2,7]`.

**Example 1:**

**Input:** nums = [10,9,2,5,3,7,101,18]

**Output:** 4

**Explanation:** The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

**Example 2:**

**Input:** nums = [0,1,0,3,2,3]

**Output:** 4

**Example 3:**

**Input:** nums = [7,7,7,7,7,7,7]

**Output:** 1

**Constraints:**

*   `1 <= nums.length <= 2500`
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

**Follow up:** Can you come up with an algorithm that runs in `O(n log(n))` time complexity?

## Solution

```racket
(require racket/list)

(define/contract (length-of-lis nums)
  (-> (listof exact-integer?) exact-integer?)
  (if (null? nums)
      0
      (let* ([dp (make-vector (+ (length nums) 1) +inf.0)]
             [left 1]
             [right 1])
        
        (for ([curr nums])
          (let ([start left]
                [end right])
            ;; Binary search for position in dp array
            (let loop ()
              (when (< (+ start 1) end)
                (let ([mid (quotient (+ start end) 2)])
                  (if (< curr (vector-ref dp mid))
                      (set! end mid)
                      (set! start mid)))
                (loop)))

            ;; Update dp array
            (cond
              [(< curr (vector-ref dp start))
               (vector-set! dp start curr)]
              [(and (> curr (vector-ref dp start))
                    (< curr (vector-ref dp end)))
               (vector-set! dp end curr)]
              [(> curr (vector-ref dp end))
               (vector-set! dp (add1 end) curr)
               (set! right (add1 right))])))

        right)))
```