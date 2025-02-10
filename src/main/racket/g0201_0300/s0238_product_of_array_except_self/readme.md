[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 238\. Product of Array Except Self

Medium

Given an integer array `nums`, return _an array_ `answer` _such that_ `answer[i]` _is equal to the product of all the elements of_ `nums` _except_ `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

**Input:** nums = [1,2,3,4]

**Output:** [24,12,8,6]

**Example 2:**

**Input:** nums = [-1,1,0,-3,3]

**Output:** [0,0,9,0,0]

**Constraints:**

*   <code>2 <= nums.length <= 10<sup>5</sup></code>
*   `-30 <= nums[i] <= 30`
*   The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

**Follow up:** Can you solve the problem in `O(1) `extra space complexity? (The output array **does not** count as extra space for space complexity analysis.)

## Solution

```racket
(define/contract (product-except-self nums)
  (-> (listof exact-integer?) (listof exact-integer?))
  (let* ((first-pass (foldl mult-w-track-zero '(1 0) nums))
	 (prod (car first-pass))
	 (zero-count (second first-pass)))
    (map (lambda (x)
	   (cond
	    [(zero? zero-count)
	     (/ prod x)]
	    [(= 1 zero-count)
	     (if (zero? x) prod 0)]
	    [else 0])) nums)))

(define (mult-w-track-zero x acc)
  (let* ((prod (car acc))
	(zero-count (second acc))
	(new-count (if (zero? x) (add1 zero-count) zero-count)))
    (list (if (= 0 x) prod (* prod x))
	  new-count)))
```