[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 221\. Maximal Square

Medium

Given an `m x n` binary `matrix` filled with `0`'s and `1`'s, _find the largest square containing only_ `1`'s _and return its area_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/max1grid.jpg)

**Input:** matrix = \[\["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]

**Output:** 4

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/26/max2grid.jpg)

**Input:** matrix = \[\["0","1"],["1","0"]]

**Output:** 1

**Example 3:**

**Input:** matrix = \[\["0"]]

**Output:** 0

**Constraints:**

*   `m == matrix.length`
*   `n == matrix[i].length`
*   `1 <= m, n <= 300`
*   `matrix[i][j]` is `'0'` or `'1'`.

## Solution

```racket
(define/contract (maximal-square matrix)
  (-> (listof (listof char?)) exact-integer?)
  (let* ([m (length matrix)]
         [n (if (zero? m) 0 (length (first matrix)))]
         [dp (make-hash)]  ; Hash table to simulate a 2D array
         [max-size 0])

    (define (get-dp i j)
      (hash-ref dp (cons i j) 0))  ; Default to 0 if not found

    ;; Iterate over the matrix
    (for ([i (in-range m)])
      (for ([j (in-range n)])
        (when (char=? (list-ref (list-ref matrix i) j) #\1)
          (let* ([min-neighbor (min (get-dp i j) (get-dp (+ i 1) j) (get-dp i (+ j 1)))]
                 [size (+ 1 min-neighbor)])
            (hash-set! dp (cons (+ i 1) (+ j 1)) size)
            (set! max-size (max max-size size))))))

    (* max-size max-size)))  ; Return area of the largest square
```