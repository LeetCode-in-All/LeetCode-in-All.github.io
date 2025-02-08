[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 152\. Maximum Product Subarray

Medium

Given an integer array `nums`, find a contiguous non-empty subarray within the array that has the largest product, and return _the product_.

The test cases are generated so that the answer will fit in a **32-bit** integer.

A **subarray** is a contiguous subsequence of the array.

**Example 1:**

**Input:** nums = [2,3,-2,4]

**Output:** 6

**Explanation:** [2,3] has the largest product 6.

**Example 2:**

**Input:** nums = [-2,0,-1]

**Output:** 0

**Explanation:** The result cannot be 2, because [-2,-1] is not a subarray.

**Constraints:**

*   <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
*   `-10 <= nums[i] <= 10`
*   The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

## Solution

```racket
(define/contract (max-product nums)
  (-> (listof exact-integer?) exact-integer?)
  (let* ([n (length nums)]
         [min-int (- (expt 2 31))])
    (let loop ([i 0]
               [start 1]
               [end 1]
               [overall-max-prod min-int])
      (if (= i n)
          overall-max-prod
          (let* ([new-start (if (zero? start) 1 start)]
                 [new-end (if (zero? end) 1 end)]
                 [start-prod (* new-start (list-ref nums i))]
                 [end-prod (* new-end (list-ref nums (- n i 1)))])
            (loop (+ i 1)
                  start-prod
                  end-prod
                  (max overall-max-prod start-prod end-prod)))))))
```