[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 22\. Generate Parentheses

Medium

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3

**Output:** ["((()))","(()())","(())()","()(())","()()()"]

**Example 2:**

**Input:** n = 1

**Output:** ["()"]

**Constraints:**

*   `1 <= n <= 8`

## Solution

```racket
(define (generate-parenthesis n)
  (let ([res '()])
    (let loop ([opening 0] [closing 0] [path ""])
      (cond ((and (= opening n) (= closing n))
             (set! res (cons path res)))
          (else
            (when (< opening n)
              (loop (add1 opening) closing (string-append path "(")))
            (when (< closing opening)
              (loop opening (add1 closing) (string-append path ")")))))
      res)))
```