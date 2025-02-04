[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 4\. Median of Two Sorted Arrays

Hard

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

**Example 1:**

**Input:** nums1 = [1,3], nums2 = [2]

**Output:** 2.00000

**Explanation:** merged array = [1,2,3] and median is 2. 

**Example 2:**

**Input:** nums1 = [1,2], nums2 = [3,4]

**Output:** 2.50000

**Explanation:** merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5. 

**Example 3:**

**Input:** nums1 = [0,0], nums2 = [0,0]

**Output:** 0.00000 

**Example 4:**

**Input:** nums1 = [], nums2 = [1]

**Output:** 1.00000 

**Example 5:**

**Input:** nums1 = [2], nums2 = []

**Output:** 2.00000 

**Constraints:**

*   `nums1.length == m`
*   `nums2.length == n`
*   `0 <= m <= 1000`
*   `0 <= n <= 1000`
*   `1 <= m + n <= 2000`
*   <code>-10<sup>6</sup> <= nums1[i], nums2[i] <= 10<sup>6</sup></code>

## Solution

```racket
(define/contract (find-median-sorted-arrays nums1 nums2)
  (-> (listof exact-integer?) (listof exact-integer?) flonum?)
  
  (define (find-kth-smallest k nums1 nums2)
    (cond
      [(empty? nums1) (list-ref nums2 k)]
      [(empty? nums2) (list-ref nums1 k)]
      [(= k 0) (min (car nums1) (car nums2))]
      [else
       (let* ([mid1 (min (length nums1) (quotient (+ k 1) 2))]
              [mid2 (min (length nums2) (quotient (+ k 1) 2))]
              [median1 (list-ref nums1 (sub1 mid1))]
              [median2 (list-ref nums2 (sub1 mid2))])
         (cond
           [(< median1 median2)
            (find-kth-smallest (- k mid1) (drop nums1 mid1) nums2)]
           [else
            (find-kth-smallest (- k mid2) nums1 (drop nums2 mid2))]))]))
  
  (define (find-median)
    (let* ([m (length nums1)]
           [n (length nums2)]
           [total-length (+ m n)]
           [half-length (quotient total-length 2)])
      (if (even? total-length)
          (/ (+ (exact->inexact (find-kth-smallest half-length nums1 nums2))
                (exact->inexact (find-kth-smallest (sub1 half-length) nums1 nums2)))
             2.0)
          (exact->inexact (find-kth-smallest half-length nums1 nums2)))))
  
  (find-median))
```