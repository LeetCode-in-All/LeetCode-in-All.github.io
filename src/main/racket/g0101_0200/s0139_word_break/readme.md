[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 139\. Word Break

Medium

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

**Input:** s = "leetcode", wordDict = ["leet","code"]

**Output:** true

**Explanation:** Return true because "leetcode" can be segmented as "leet code".

**Example 2:**

**Input:** s = "applepenapple", wordDict = ["apple","pen"]

**Output:** true

**Explanation:** Return true because "applepenapple" can be segmented as "apple pen apple". 

Note that you are allowed to reuse a dictionary word.

**Example 3:**

**Input:** s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]

**Output:** false

**Constraints:**

*   `1 <= s.length <= 300`
*   `1 <= wordDict.length <= 1000`
*   `1 <= wordDict[i].length <= 20`
*   `s` and `wordDict[i]` consist of only lowercase English letters.
*   All the strings of `wordDict` are **unique**.

## Solution

```racket
(define/contract (word-break s wordDict)
  (-> string? (listof string?) boolean?)
  (let ((memo (make-hash)))
    (define (dp i)
      (cond
        [(= i (string-length s)) #t]
        [(hash-has-key? memo i) (hash-ref memo i)]
        [else
         (let loop ((words wordDict))
           (if (null? words)
               (begin (hash-set! memo i #f) #f)
               (let* ((word (car words))
                      (len (string-length word)))
                 (if (and (<= (+ i len) (string-length s))
                          (string=? (substring s i (+ i len)) word)
                          (dp (+ i len)))
                     (begin (hash-set! memo i #t) #t)
                     (loop (cdr words))))))]))
    (dp 0)))
```