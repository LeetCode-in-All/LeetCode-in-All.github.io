[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 394\. Decode String

Medium

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed <code>10<sup>5</sup></code>.

**Example 1:**

**Input:** s = "3[a]2[bc]"

**Output:** "aaabcbc"

**Example 2:**

**Input:** s = "3[a2[c]]"

**Output:** "accaccacc"

**Example 3:**

**Input:** s = "2[abc]3[cd]ef"

**Output:** "abcabccdcdcdef"

**Constraints:**

*   `1 <= s.length <= 30`
*   `s` consists of lowercase English letters, digits, and square brackets `'[]'`.
*   `s` is guaranteed to be **a valid** input.
*   All the integers in `s` are in the range `[1, 300]`.

## Solution

```racket
(define/contract (decode-string s)
  (-> string? string?)
  (let-values ([(result _) (decode-helper (string->list s) 0)])
    result))

(define (decode-helper chars pos)
  (let loop ([current-pos pos]
             [count 0]
             [result ""])
    (if (>= current-pos (length chars))
        (values result current-pos)
        (let ([char (list-ref chars current-pos)])
          (cond
            ; If it's a letter, append it to result
            [(char-alphabetic? char)
             (loop (add1 current-pos)
                   count
                   (string-append result (string char)))]
            
            ; If it's a digit, update count
            [(char-numeric? char)
             (loop (add1 current-pos)
                   (+ (* count 10) (- (char->integer char) (char->integer #\0)))
                   result)]
            
            ; If it's '[', handle nested string
            [(char=? char #\[)
             (let-values ([(nested-str new-pos) (decode-helper chars (add1 current-pos))])
               (loop new-pos
                     0
                     (string-append result 
                                  (string-join 
                                   (make-list count nested-str)
                                   ""))))]
            
            ; If it's ']', return current result and position
            [(char=? char #\])
             (values result (add1 current-pos))]
            
            ; Skip other characters
            [else (loop (add1 current-pos) count result)])))))
```