[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 438\. Find All Anagrams in a String

Medium

Given two strings `s` and `p`, return _an array of all the start indices of_ `p`_'s anagrams in_ `s`. You may return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** s = "cbaebabacd", p = "abc"

**Output:** [0,6]

**Explanation:** 

The substring with start index = 0 is "cba", which is an anagram of "abc". 

The substring with start index = 6 is "bac", which is an anagram of "abc".

**Example 2:**

**Input:** s = "abab", p = "ab"

**Output:** [0,1,2]

**Explanation:** 

The substring with start index = 0 is "ab", which is an anagram of "ab". 

The substring with start index = 1 is "ba", which is an anagram of "ab". 

The substring with start index = 2 is "ab", which is an anagram of "ab".

**Constraints:**

*   <code>1 <= s.length, p.length <= 3 * 10<sup>4</sup></code>
*   `s` and `p` consist of lowercase English letters.

## Solution

```racket
(define/contract (find-anagrams s p)
  (-> string? string? (listof exact-integer?))
  
  ; Initialize character frequency map for pattern p
  (let ([char-map (make-vector 26 0)])
    ; Fill the character map with pattern frequencies
    (for ([c (string->list p)])
      (vector-set! char-map 
                   (- (char->integer c) (char->integer #\a))
                   (add1 (vector-ref char-map (- (char->integer c) (char->integer #\a))))))
    
    ; Helper function to check if current window is an anagram
    (define (is-anagram? map)
      (for/and ([count (in-vector map)])
        (zero? count)))
    
    ; Main sliding window loop
    (let loop ([i 0]           ; Current position
               [j 0]           ; Window start
               [curr-map char-map]
               [result '()])
      (if (>= i (string-length s))
          (reverse result)
          (let* ([curr-char (string-ref s i)]
                 [curr-idx (- (char->integer curr-char) (char->integer #\a))]
                 ; Update map with current character
                 [new-map (let ([temp-map (vector-copy curr-map)])
                           (vector-set! temp-map curr-idx (sub1 (vector-ref temp-map curr-idx)))
                           temp-map)]
                 ; Update map by removing leftmost character if window is too large
                 [final-map (if (>= i (string-length p))
                               (let ([left-char (string-ref s j)]
                                    [temp-map (vector-copy new-map)])
                                 (vector-set! temp-map 
                                            (- (char->integer left-char) (char->integer #\a))
                                            (add1 (vector-ref temp-map 
                                                            (- (char->integer left-char) 
                                                               (char->integer #\a)))))
                                 temp-map)
                               new-map)]
                 [next-j (if (>= i (string-length p)) (add1 j) j)])
            
            (loop (add1 i)
                  next-j
                  final-map
                  (if (and (>= i (sub1 (string-length p)))
                          (is-anagram? final-map))
                      (cons next-j result)
                      result)))))))
```