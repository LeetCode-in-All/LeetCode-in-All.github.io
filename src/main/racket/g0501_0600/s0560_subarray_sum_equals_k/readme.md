[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 560\. Subarray Sum Equals K

Medium

Given an array of integers `nums` and an integer `k`, return _the total number of subarrays whose sum equals to_ `k`.

A subarray is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**

**Input:** nums = [1,1,1], k = 2

**Output:** 2

**Example 2:**

**Input:** nums = [1,2,3], k = 3

**Output:** 2

**Constraints:**

*   <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
*   `-1000 <= nums[i] <= 1000`
*   <code>-10<sup>7</sup> <= k <= 10<sup>7</sup></code>

## Solution

```racket
(define/contract (subarray-sum nums k)
  (-> (listof exact-integer?) exact-integer? exact-integer?)
  (let ([temp-sum 0]
        [result 0]
        [sum-count (make-hash)])
    
    ; Initialize the hash with 0 sum occurring once
    (hash-set! sum-count 0 1)
    
    ; Process each number
    (for ([num nums])
      ; Update running sum
      (set! temp-sum (+ temp-sum num))
      
      ; Check if we have seen temp-sum - k before
      (when (hash-has-key? sum-count (- temp-sum k))
        (set! result (+ result (hash-ref sum-count (- temp-sum k)))))
      
      ; Update the count for current sum
      (hash-set! sum-count 
                 temp-sum 
                 (add1 (hash-ref sum-count temp-sum 0))))
    
    result))
```