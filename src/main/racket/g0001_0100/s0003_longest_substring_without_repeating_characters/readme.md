[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 3\. Longest Substring Without Repeating Characters

Medium

Given a string `s`, find the length of the **longest substring** without repeating characters.

**Example 1:**

**Input:** s = "abcabcbb"

**Output:** 3

**Explanation:** The answer is "abc", with the length of 3. 

**Example 2:**

**Input:** s = "bbbbb"

**Output:** 1

**Explanation:** The answer is "b", with the length of 1. 

**Example 3:**

**Input:** s = "pwwkew"

**Output:** 3

**Explanation:** The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring. 

**Example 4:**

**Input:** s = ""

**Output:** 0 

**Constraints:**

*   <code>0 <= s.length <= 5 * 10<sup>4</sup></code>
*   `s` consists of English letters, digits, symbols and spaces.

## Solution

```racket
; Helper function to get the sublist up to 'v' excluded.
(define (take-till q v)
  (define (take-till/helper q v acc)
    (if (or (null? q)
            (eq? (car q) v))
        acc
        (take-till/helper (cdr q) v (cons (car q) acc))))
  (foldl cons null (take-till/helper q v null)))

; (take-till '(1 2 3 4 5) 4) returns '(1 2 3)

(define (max-substr s queue len max-len)
  (cond
    [(null? s) max-len]
    [(pair? s)
     (let ((x (car s))
           (xs (cdr s)))
       (if (member x queue)
           (let* ((tqueue (take-till queue x)) ; queue from last repeated char
                 (tqueue-len (+ 1 (length tqueue))))
             (max-substr xs (cons x tqueue) tqueue-len (max tqueue-len max-len)))
           ; else
           (max-substr xs (cons x queue) (+ 1 len) (max (+ 1 len) max-len))))]))

(define/contract (length-of-longest-substring s)
  (-> string? exact-integer?)
  (max-substr (string->list s) null 0 0))
```