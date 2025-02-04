[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 20\. Valid Parentheses

Easy

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1.  Open brackets must be closed by the same type of brackets.
2.  Open brackets must be closed in the correct order.

**Example 1:**

**Input:** s = "()"

**Output:** true

**Example 2:**

**Input:** s = "()[]{}"

**Output:** true

**Example 3:**

**Input:** s = "(]"

**Output:** false

**Example 4:**

**Input:** s = "([)]"

**Output:** false

**Example 5:**

**Input:** s = "{[]}"

**Output:** true

**Constraints:**

*   <code>1 <= s.length <= 10<sup>4</sup></code>
*   `s` consists of parentheses only `'()[]{}'`.

## Solution

```racket
(define (is-left-paren c)
    (or (eq? c #\u28)
        (eq? c #\[)
        (eq? c #\{)))

(define (right-paren c)
    (cond ((eq? c #\u28) #\u29)
          ((eq? c #\[) #\])
          ((eq? c #\{) #\})))

(define/contract (is-valid s)
  (-> string? boolean?)
  (define (loop s stack)
    (if (= 0 (string-length s))
        (null? stack)
        (let ()
            (define c (string-ref s 0))
            (define remain (substring s 1))
            (if (is-left-paren c)
                (loop remain (cons c stack))
                (if (null? stack)
                    #f
                    (let ()
                        (define stack-top (car stack))
                        (if (eq? c (right-paren stack-top))
                            (loop remain (cdr stack))
                            #f)))))))
  (loop s '()))
```