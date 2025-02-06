[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 72\. Edit Distance

Hard

Given two strings `word1` and `word2`, return _the minimum number of operations required to convert `word1` to `word2`_.

You have the following three operations permitted on a word:

*   Insert a character
*   Delete a character
*   Replace a character

**Example 1:**

**Input:** word1 = "horse", word2 = "ros"

**Output:** 3

**Explanation:** 

horse -> rorse (replace 'h' with 'r') 

rorse -> rose (remove 'r') 

rose -> ros (remove 'e')

**Example 2:**

**Input:** word1 = "intention", word2 = "execution"

**Output:** 5

**Explanation:** 

intention -> inention (remove 't') 

inention -> enention (replace 'i' with 'e') 

enention -> exention (replace 'n' with 'x') 

exention -> exection (replace 'n' with 'c') 

exection -> execution (insert 'u')

**Constraints:**

*   `0 <= word1.length, word2.length <= 500`
*   `word1` and `word2` consist of lowercase English letters.

## Solution

```racket
(define/contract (min-distance word1 word2)
  (-> string? string? exact-integer?)
  (let* ((n1 (string-length word1))
         (n2 (string-length word2)))
    (if (> n2 n1)
        (min-distance word2 word1)
        (let ((dp (make-vector (+ n2 1) 0)))
          (for ([j (in-range (+ n2 1))])
            (vector-set! dp j j))
          (for ([i (in-range 1 (+ n1 1))])
            (let ((pre (vector-ref dp 0)))
              (vector-set! dp 0 i)
              (for ([j (in-range 1 (+ n2 1))])
                (let* ((tmp (vector-ref dp j))
                       (cost (if (char=? (string-ref word1 (- i 1)) (string-ref word2 (- j 1)))
                                 pre
                                 (+ 1 (min pre (vector-ref dp j) (vector-ref dp (- j 1)))))))
                  (vector-set! dp j cost)
                  (set! pre tmp)))))
          (vector-ref dp n2)))))
```