[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 84\. Largest Rectangle in Histogram

Hard

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return _the area of the largest rectangle in the histogram_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

**Input:** heights = [2,1,5,6,2,3]

**Output:** 10

**Explanation:** The above is a histogram where width of each bar is 1. 

The largest rectangle is shown in the red area, which has an area = 10 units.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

**Input:** heights = [2,4]

**Output:** 4

**Constraints:**

*   <code>1 <= heights.length <= 10<sup>5</sup></code>
*   <code>0 <= heights[i] <= 10<sup>4</sup></code>

## Solution

```racket
(define/contract (largest-rectangle-area heights)
  (-> (listof exact-integer?) exact-integer?)
  (let* ((n (length heights))
         (heights-vec (list->vector (append heights '(0))))
         (stack '())
         (max-area 0))
    
    (for ([i (in-range (add1 n))])
      (let loop ()
        (when (and (not (null? stack))
                   (<= (vector-ref heights-vec i) (vector-ref heights-vec (car stack))))
          (let* ((top (car stack))
                 (new-stack (cdr stack))
                 (height (vector-ref heights-vec top))
                 (width (if (null? new-stack) i (- i (car new-stack) 1)))
                 (area (* height width)))
            (set! max-area (max max-area area))
            (set! stack new-stack)
            (loop))))
      (set! stack (cons i stack)))

    max-area))
```