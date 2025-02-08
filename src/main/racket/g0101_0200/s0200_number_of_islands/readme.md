[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 200\. Number of Islands

Medium

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

**Input:** grid = [ 

["1","1","1","1","0"], 

["1","1","0","1","0"], 

["1","1","0","0","0"], 

["0","0","0","0","0"] 

]

**Output:** 1

**Example 2:**

**Input:** grid = [ 

["1","1","0","0","0"], 

["1","1","0","0","0"], 

["0","0","1","0","0"], 

["0","0","0","1","1"] 

]

**Output:** 3

**Constraints:**

*   `m == grid.length`
*   `n == grid[i].length`
*   `1 <= m, n <= 300`
*   `grid[i][j]` is `'0'` or `'1'`.

## Solution

```racket
(define-syntax vref
  (syntax-rules ()
    ((_ vec idx) (vector-ref vec idx))))

(define-syntax vlen
  (syntax-rules ()
    ((_ vec) (vector-length vec))))

(define-syntax in?
  (syntax-rules ()
    ((_ st x) (set-member? st x))))

(define (num-islands grid)
  (define g (list->vector (map list->vector grid)))

  (define (dfs i j visited)
    (cond
      [(or (< i 0) (>= i (vlen g)) (< j 0) (>= j (vlen (vref g 0)))) visited] ; if i,j is out of bounds
      [(in? visited (cons i j)) visited]
      [(equal? (vref (vref g i) j) #\0) visited]
      [else (dfs i (sub1 j) (dfs (add1 i) j (dfs i (add1 j) (dfs (sub1 i) j (set-add visited (cons i j))))))])) ; explore all 4 directions

  (for*/fold ([islands 0]
              [visited (set)]
              #:result islands)
             ([i (vlen g)]
              [j (vlen (vref g 0))])
    (match (vref (vref g i) j)
      [#\0 (values islands visited)]
      [#\1 #:when (in? visited (cons i j)) (values islands visited)]
      [#\1 (values (add1 islands) (dfs i j visited))])))
```