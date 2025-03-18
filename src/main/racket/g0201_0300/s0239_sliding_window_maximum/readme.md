[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 239\. Sliding Window Maximum

Hard

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

**Example 1:**

**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3

**Output:** [3,3,5,5,6,7]

**Explanation:** 

Window position Max 

--------------- ----- 

[1 3 -1] -3 5 3 6 7 **3** 

1 [3 -1 -3] 5 3 6 7 **3** 

1 3 [-1 -3 5] 3 6 7 **5** 

1 3 -1 [-3 5 3] 6 7 **5** 

1 3 -1 -3 [5 3 6] 7 **6** 

1 3 -1 -3 5 [3 6 7] **7**

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1]

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `1 <= k <= nums.length`

## Solution

```racket
(require racket/contract)

(define/contract (max-sliding-window nums k)
  (-> (listof exact-integer?) exact-integer? (listof exact-integer?))
  (if (= k 1)
      nums ; Special case where each window is just a single number
      (let* ([n (length nums)]
             [nums-vec (list->vector nums)]
             [capacity n]
             [dq (make-vector capacity 0)]
             [head (box 0)]
             [tail (box 0)]
             [result '()])

        ;; Helper functions for deque operations
        (define (deque-empty?) (= (unbox head) (unbox tail)))
        (define (deque-push-back! idx)
          (vector-set! dq (unbox tail) idx)
          (set-box! tail (modulo (+ (unbox tail) 1) capacity)))
        (define (deque-pop-back!)
          (set-box! tail (modulo (- (unbox tail) 1) capacity)))
        (define (deque-front) (vector-ref dq (unbox head)))
        (define (deque-pop-front!)
          (set-box! head (modulo (+ (unbox head) 1) capacity)))
        (define (deque-back)
          (vector-ref dq (if (= (unbox tail) 0) (- capacity 1) (- (unbox tail) 1))))
        (define (pop-back-while cur)
          (when (not (deque-empty?))
            (when (< (vector-ref nums-vec (deque-back)) cur)
              (deque-pop-back!)
              (pop-back-while cur))))

        ;; Iterate through nums
        (for ([idx (in-range n)])
          (let ([cur (vector-ref nums-vec idx)])
            (pop-back-while cur)
            (deque-push-back! idx)
            (when (and (>= idx k)
                       (not (deque-empty?))
                       (equal? (deque-front) (- idx k)))
              (deque-pop-front!))
            (when (>= idx (sub1 k))
              (set! result (cons (vector-ref nums-vec (deque-front)) result)))))

        (reverse result))))
```