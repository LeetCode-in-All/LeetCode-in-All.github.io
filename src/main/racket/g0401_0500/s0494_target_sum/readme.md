[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 494\. Target Sum

Medium

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

*   For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

**Example 1:**

**Input:** nums = [1,1,1,1,1], target = 3

**Output:** 5

**Explanation:** There are 5 ways to assign symbols to make the sum of nums be target 3. 

-1 + 1 + 1 + 1 + 1 = 3 

+1 - 1 + 1 + 1 + 1 = 3 

+1 + 1 - 1 + 1 + 1 = 3 

+1 + 1 + 1 - 1 + 1 = 3 

    +1 + 1 + 1 + 1 - 1 = 3

**Example 2:**

**Input:** nums = [1], target = 1

**Output:** 1

**Constraints:**

*   `1 <= nums.length <= 20`
*   `0 <= nums[i] <= 1000`
*   `0 <= sum(nums[i]) <= 1000`
*   `-1000 <= target <= 1000`

## Solution

```racket
(define/contract (find-target-sum-ways nums target)
  (-> (listof exact-integer?) exact-integer? exact-integer?)
  (if (null? nums)
      0  ; Handle empty list case
      (let* ([total-sum (apply + nums)]
             [sum (- total-sum target)])
        (if (or (negative? sum) (odd? sum))
            0
            (solve nums (quotient sum 2))))))

(define (solve nums target)
  (if (null? nums)
      0
      (let* ([first-num (car nums)]
             ; Initialize prev array with proper size
             [prev (make-vector (add1 target) 0)])
        
        ; Handle base cases for first number
        (vector-set! prev 0 
                     (if (zero? first-num) 2 1))
        (when (and (not (zero? first-num))
                   (<= first-num target))
          (vector-set! prev first-num 1))
        
        ; Process rest of the numbers
        (for ([num (in-list (cdr nums))])
          (let ([curr (make-vector (add1 target) 0)])
            (for ([j (in-range (add1 target))])
              (let ([taken (if (>= j num)
                              (vector-ref prev (- j num))
                              0)]
                    [non-taken (vector-ref prev j)])
                (vector-set! curr j (+ taken non-taken))))
            ; Update prev for next iteration
            (for ([j (in-range (add1 target))])
              (vector-set! prev j (vector-ref curr j)))))
        
        ; Return final result
        (vector-ref prev target))))
```