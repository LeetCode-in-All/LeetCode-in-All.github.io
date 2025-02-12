[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 763\. Partition Labels

Medium

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return _a list of integers representing the size of these parts_.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"

**Output:** [9,7,8]

**Explanation:** The partition is "ababcbaca", "defegde", "hijhklij". This is a partition so that each letter appears in at most one part. A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.

**Example 2:**

**Input:** s = "eccbbbbdec"

**Output:** [10]

**Constraints:**

*   `1 <= s.length <= 500`
*   `s` consists of lowercase English letters.

## Solution

```racket
(define/contract (partition-labels s)
  (-> string? (listof exact-integer?))
  (let* ([chars (string->list s)]
         [position (make-vector 26 0)])
    
    ; First pass: record last position of each character
    (for ([c chars]
          [i (in-range (string-length s))])
      (vector-set! position 
                   (- (char->integer c) (char->integer #\a))
                   i))
    
    ; Second pass: find partitions
    (let loop ([i 0]
               [prev -1]
               [max-pos 0]
               [result '()])
      (if (>= i (string-length s))
          (reverse result)
          (let* ([curr-char (string-ref s i)]
                 [curr-last-pos (vector-ref position 
                                          (- (char->integer curr-char) 
                                             (char->integer #\a)))]
                 [new-max (max max-pos curr-last-pos)])
            (if (= i new-max)
                (loop (add1 i)
                      i
                      new-max
                      (cons (- i prev) result))
                (loop (add1 i)
                      prev
                      new-max
                      result)))))))
```