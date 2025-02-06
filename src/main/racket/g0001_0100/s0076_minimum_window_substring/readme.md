[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 76\. Minimum Window Substring

Hard

Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window substring** of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window. If there is no such substring__, return the empty string_ `""`_._

The testcases will be generated such that the answer is **unique**.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "ADOBECODEBANC", t = "ABC"

**Output:** "BANC"

**Explanation:** The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

**Example 2:**

**Input:** s = "a", t = "a"

**Output:** "a"

**Explanation:** The entire string s is the minimum window.

**Example 3:**

**Input:** s = "a", t = "aa"

**Output:** ""

**Explanation:** Both 'a's from t must be included in the window. Since the largest window of s only has one 'a', return empty string.

**Constraints:**

*   `m == s.length`
*   `n == t.length`
*   <code>1 <= m, n <= 10<sup>5</sup></code>
*   `s` and `t` consist of uppercase and lowercase English letters.

**Follow up:** Could you find an algorithm that runs in `O(m + n)` time?

## Solution

```racket
(define (zip lst1 lst2)
  (map cons lst1 lst2))

(define (make-zero-hash lst)
  (make-immutable-hash (zip lst (make-list (length lst) 0))))

(define (hash-inc k ht)
  (hash-update ht k add1 0))

(define (safe-hash-inc k ht)
  (if (hash-ref ht k #f) (hash-update ht k add1) ht))

(define (safe-hash-dec k ht)
  (if (hash-ref ht k #f) (hash-update ht k sub1) ht))

(define (frequencies lst)
  (foldl hash-inc (hash) lst))

(define (pair-min l1 r1 l2 r2)
  (if (< (- r1 l1) (- r2 l2)) (values l1 r1) (values l2 r2)))

(define (sref s i) (string-ref s (min (sub1 (string-length s)) i)))

(define (min-window s t)
  (define t-lst (string->list t))

  (define target (frequencies t-lst))

  (define (delta-dec delta seen c)
    (cond
      [(and (hash-ref target c #f) 
            (< (hash-ref seen c) (hash-ref target c)))
       (sub1 delta)]
      [else delta]))
  
  (define (delta-inc delta seen c)
    (cond 
      [(and (hash-ref target c #f)
            (<= (hash-ref seen c) (hash-ref target c)))
       (add1 delta)]
      [else delta]))

  (let loop ([l 0] [r 0] [seen (make-zero-hash t-lst)] 
             [delta (length t-lst)] [sl 0] [sr 0])
    (define-values (left-char right-char) (values (sref s l) (sref s r)))
    (define-values (l* r*) (pair-min l r sl sr))
    (cond
      [(and (= 0 sr) 
            (= delta 0))
       (loop (add1 l) r (safe-hash-dec left-char seen)
             (delta-inc delta seen left-char) l r)]
      [(and (= r (string-length s)) (= delta 0)) 
       (loop (add1 l) r (safe-hash-dec left-char seen) 
             (delta-inc delta seen left-char) l* r*)]
      [(= r (string-length s)) 
       (substring s sl sr)]
      [(= delta 0)
       (loop (add1 l) r (safe-hash-dec left-char seen)
             (delta-inc delta seen left-char) l* r*)]
      [else
       (loop l (add1 r) (safe-hash-inc right-char seen) 
             (delta-dec delta seen right-char) sl sr)])))
```