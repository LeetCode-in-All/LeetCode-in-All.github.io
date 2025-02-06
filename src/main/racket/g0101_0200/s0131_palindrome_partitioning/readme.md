[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 131\. Palindrome Partitioning

Medium

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

**Example 1:**

**Input:** s = "aab"

**Output:** [["a","a","b"],["aa","b"]]

**Example 2:**

**Input:** s = "a"

**Output:** [["a"]]

**Constraints:**

*   `1 <= s.length <= 16`
*   `s` contains only lowercase English letters.

## Solution

```racket
(define/contract (partition s)
  (-> string? (listof (listof string?)))
  (define res '())
  (define (backtracking currArr start)
    (if (= start (string-length s))
        (set! res (cons (reverse currArr) res))
        (for ([end (in-range start (string-length s))])
          (when (is-palindrome? s start end)
            (backtracking (cons (substring s start (add1 end)) currArr) (add1 end))))))
  (backtracking '() 0)
  res)

(define (is-palindrome? s start end)
  (let loop ((i start) (j end))
    (or (>= i j)
        (and (char=? (string-ref s i) (string-ref s j))
             (loop (add1 i) (sub1 j))))))
```