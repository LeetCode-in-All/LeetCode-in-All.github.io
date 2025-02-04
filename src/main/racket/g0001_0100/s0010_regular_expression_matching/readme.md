[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 10\. Regular Expression Matching

Hard

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:

*   `'.'` Matches any single character.
*   `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

**Example 1:**

**Input:** s = "aa", p = "a"

**Output:** false

**Explanation:** "a" does not match the entire string "aa". 

**Example 2:**

**Input:** s = "aa", p = "a\*"

**Output:** true

**Explanation:** '\*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa". 

**Example 3:**

**Input:** s = "ab", p = ".\*"

**Output:** true

**Explanation:** ".\*" means "zero or more (\*) of any character (.)". 

**Example 4:**

**Input:** s = "aab", p = "c\*a\*b"

**Output:** true

**Explanation:** c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab". 

**Example 5:**

**Input:** s = "mississippi", p = "mis\*is\*p\*."

**Output:** false 

**Constraints:**

*   `1 <= s.length <= 20`
*   `1 <= p.length <= 30`
*   `s` contains only lowercase English letters.
*   `p` contains only lowercase English letters, `'.'`, and `'*'`.
*   It is guaranteed for each appearance of the character `'*'`, there will be a previous valid character to match.

## Solution

```racket
(define (regex-state s is-star)
  (list s (if is-star '* '1)))

(define (regex-state-string ps)
  (car ps))

(define (regex-state-star? ps)
  (eq? (cadr ps) '*))

(define (regex-state-single-char? ps)
  (eq? (cadr ps) '1))

(define (parse-regex regex)
  (cond [(eq? (string-length regex) 0) '()]
        [(eq? (string-length regex) 1) (list (regex-state regex #f))]
        [(eq? (string-ref regex 1) #\*)
            (cons (regex-state (substring regex 0 1) #t) (parse-regex (substring regex 2)))]
        [else
         (cons (regex-state (substring regex 0 1) #f) (parse-regex (substring regex 1)))]))

; Collapse repeated star statements. "a*a*" is the same as "a*"
(define (optimized-parsed-regex parsed-regex)
  (cond ([empty? parsed-regex] '())
        ([= (length parsed-regex) 1] parsed-regex)
        ([and
          (regex-state-star? (car parsed-regex))
          (regex-state-star? (cadr parsed-regex))
          (string=? (regex-state-string (car parsed-regex))
                    (regex-state-string (cadr parsed-regex)))]                
         (cons (car parsed-regex) (optimized-parsed-regex (cddr parsed-regex))))
        (else
         (cons (car parsed-regex) (optimized-parsed-regex (cdr parsed-regex))))))
(define (match-regex-part s p)
  (cond ([empty? p] #f)
        ([= (string-length s) 0] (regex-state-star? p))
        ([= (string-length s) 1]
         (or (string=? "." (car p)) (string=? s (regex-state-string p))))
        (else #f)))

(define (first-part-of-string s)
  (if (= (string-length s) 0) "" (substring s 0 1)))
(define (reduce-string s)
  (if (= (string-length s) 0) "" (substring s 1)))

(define (is-match-regex-parsed s parsed-exp)
  (cond ([= (string-length s) 0]
         (or
          (= (length parsed-exp) 0)
          (andmap regex-state-star? parsed-exp)))
        ([= (length parsed-exp) 0] (= (string-length s) 0))
        ([regex-state-single-char? (car parsed-exp)]
         (if (match-regex-part (first-part-of-string s) (car parsed-exp))
             (is-match-regex-parsed (reduce-string s) (cdr parsed-exp))
             #f))             
        ([regex-state-star? (car parsed-exp)]
         (or
          (is-match-regex-parsed s (cdr parsed-exp))
          (if (match-regex-part (first-part-of-string s) (car parsed-exp))
              (is-match-regex-parsed (reduce-string s) parsed-exp)
              #f)))            
        (else 'error)))
        

(define/contract (is-match s p)
  (-> string? string? boolean?)
  (is-match-regex-parsed s (optimized-parsed-regex (parse-regex p))))
```