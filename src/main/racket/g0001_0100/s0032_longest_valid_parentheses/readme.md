[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 32\. Longest Valid Parentheses

Hard

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

**Example 1:**

**Input:** s = "(()"

**Output:** 2

**Explanation:** The longest valid parentheses substring is "()".

**Example 2:**

**Input:** s = ")()())"

**Output:** 4

**Explanation:** The longest valid parentheses substring is "()()".

**Example 3:**

**Input:** s = ""

**Output:** 0

**Constraints:**

*   <code>0 <= s.length <= 3 * 10<sup>4</sup></code>
*   `s[i]` is `'('`, or `')'`.

## Solution

```racket
(define/contract (longest-valid-parentheses s)
  (-> string? exact-integer?)
  (let* ((n (string-length s)))
    (define (scan direction)
      (let loop ((i (if direction 0 (- n 1)))
                 (left 0) (right 0) (max-val 0))
        (if (or (< i 0) (>= i n))
            max-val
            (let* ((ch (string-ref s i))
                   (left (if (char=? ch #\() (+ left 1) left))
                   (right (if (char=? ch #\)) (+ right 1) right)))
              (cond
                ((and direction (> right left)) (loop (+ i 1) 0 0 max-val))
                ((and (not direction) (> left right)) (loop (- i 1) 0 0 max-val))
                ((= left right) (loop (+ (if direction 1 -1) i) left right (max max-val (+ left right))))
                (else (loop (+ (if direction 1 -1) i) left right max-val)))))))
    (max (scan #t) (scan #f))))
```