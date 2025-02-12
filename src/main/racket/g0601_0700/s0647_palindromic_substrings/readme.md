[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 647\. Palindromic Substrings

Medium

Given a string `s`, return _the number of **palindromic substrings** in it_.

A string is a **palindrome** when it reads the same backward as forward.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "abc"

**Output:** 3

**Explanation:** Three palindromic strings: "a", "b", "c".

**Example 2:**

**Input:** s = "aaa"

**Output:** 6

**Explanation:** Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consists of lowercase English letters.

## Solution

```racket
(define (check-polin vec left right)
  (cond [(< left 0) 0]
        [(>= right (vector-length vec)) 0]
        [(not (eq? (vector-ref vec left) (vector-ref vec right))) 0]
        [else (add1 (check-polin vec (sub1 left) (add1 right)))]))

(define (count-substrings s)
  (let ([vec (list->vector (string->list s))]
        [len (string-length s)])
    (apply + (for/list ([i (range len)])
           (+ 1
                (check-polin vec (sub1 i) (add1 i))
                (check-polin vec (sub1 i) i))))))
```