[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 70\. Climbing Stairs

Easy

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**

**Input:** n = 2

**Output:** 2

**Explanation:** There are two ways to climb to the top. 

1. 1 step + 1 step 

2. 2 steps

**Example 2:**

**Input:** n = 3

**Output:** 3

**Explanation:** There are three ways to climb to the top. 

1. 1 step + 1 step + 1 step 

2. 1 step + 2 steps 

3. 2 steps + 1 step

**Constraints:**

*   `1 <= n <= 45`

## Solution

```racket
(define (clmHelp n hTable)
	(cond
		; base cases
		((= 1 n) 1)
		((= 2 n) 2)
		((hash-ref hTable n #f) (hash-ref hTable n))

		; inductive case
		(else
			(let*
				; the local variables
				(
					(a (clmHelp (- n 1) hTable))
					(b (clmHelp (- n 2) hTable))
					(numPos (+ a b))
				)

				; the body
				(hash-set! hTable n numPos)
				numPos
			)
		)
	)
)

(define/contract (climb-stairs n)
	(-> exact-integer? exact-integer?)
	(local
		; local definitions
		((define hTable (make-hash)))

		; function body
		(clmHelp n hTable)
	)
)
```