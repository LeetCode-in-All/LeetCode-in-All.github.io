[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 5\. Longest Palindromic Substring

Medium

Given a string `s`, return _the longest palindromic substring_ in `s`.

**Example 1:**

**Input:** s = "babad"

**Output:** "bab" **Note:** "aba" is also a valid answer. 

**Example 2:**

**Input:** s = "cbbd"

**Output:** "bb" 

**Example 3:**

**Input:** s = "a"

**Output:** "a" 

**Example 4:**

**Input:** s = "ac"

**Output:** "a" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consist of only digits and English letters.

## Solution

```racket
(define (longest-palindrome s)
  (define (expand-around-center s left right)
    (let loop ([l left] [r right])
      (if (and (>= l 0)
               (< r (string-length s))
               (char=? (string-ref s l) (string-ref s r)))
          (loop (sub1 l) (add1 r))
          (values (add1 l) (sub1 r))))) ;; Return correct boundaries

  (define (find-longest-palindrome s)
    (define len (string-length s))
    (define start 0)
    (define end 0)
    (for ([i (in-range len)])
      ;; Odd-length palindromes centered at i
      (define-values (l1 r1) (expand-around-center s i i))
      ;; Even-length palindromes centered between i and i + 1
      (define-values (l2 r2) (expand-around-center s i (add1 i)))
      
      ;; Update the maximum length palindrome if necessary
      (when (> (- r1 l1) (- end start))
        (set! start l1)
        (set! end r1))
      (when (> (- r2 l2) (- end start))
        (set! start l2)
        (set! end r2)))
    (substring s start (add1 end))) 

  (find-longest-palindrome s))
```