[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 64\. Minimum Path Sum

Medium

Given a `m x n` `grid` filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

**Input:** grid = \[\[1,3,1],[1,5,1],[4,2,1]]

**Output:** 7

**Explanation:** Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.

**Example 2:**

**Input:** grid = \[\[1,2,3],[4,5,6]]

**Output:** 12

**Constraints:**

*   `m == grid.length`
*   `n == grid[i].length`
*   `1 <= m, n <= 200`
*   `0 <= grid[i][j] <= 100`

## Solution

```racket
; dynamic programming helper function
(define (mpsAux grid curpos dpTable ub)
	(local
		[(define (get grid pos) (list-ref (list-ref grid (car pos)) (cdr pos)))]
		(cond
			; return start value
			[(equal? curpos (cons 0 0)) (car (car grid))]

			; handle out of bounds
			[(or (< (car curpos) 0) (< (cdr curpos) 0)) +inf.0]

			; position appeared before
			[(hash-ref dpTable curpos #f) (hash-ref dpTable curpos)]

			; inductive case
			[else
				(let*
					(
						; go up
						[u_val (mpsAux grid (cons (- (car curpos) 1) (cdr curpos)) dpTable ub)]

						; go left 
						[l_val (mpsAux grid (cons (car curpos) (- (cdr curpos) 1)) dpTable ub)]

						; compute the current least cost
						[cur-least-cost (+ (get grid curpos) (min u_val l_val))]
					)
					(hash-set! dpTable curpos cur-least-cost)
					cur-least-cost
				)
			]
		)
	)
)

; the (x . y) position of the grid is the x'th row and y'th column of the grid
(define/contract (min-path-sum grid)
	(-> (listof (listof exact-integer?)) exact-integer?)
	(local
		[(define dpTable (make-hash))]
		(let*
			(
				[curpos (cons (- (length grid) 1) (- (length (car grid)) 1))]
				[least-val (mpsAux grid curpos dpTable 200)]
			)
			(inexact->exact least-val)
		)
	)
)
```