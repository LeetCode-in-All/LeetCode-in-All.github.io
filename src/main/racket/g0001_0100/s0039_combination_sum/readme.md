[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 39\. Combination Sum

Medium

Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is **guaranteed** that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

**Example 1:**

**Input:** candidates = [2,3,6,7], target = 7

**Output:** [[2,2,3],[7]]

**Explanation:** 
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.

7 is a candidate, and 7 = 7. 

These are the only two combinations.

**Example 2:**

**Input:** candidates = [2,3,5], target = 8

**Output:** [[2,2,2,2],[2,3,3],[3,5]]

**Example 3:**

**Input:** candidates = [2], target = 1

**Output:** []

**Constraints:**

*   `1 <= candidates.length <= 30`
*   `1 <= candidates[i] <= 200`
*   All elements of `candidates` are **distinct**.
*   `1 <= target <= 500`

## Solution

```racket
(define (create-task-rec elems target next-list result)
  (if (= 0 (length next-list)) result
      (if (< target (+ (foldl + 0 elems) (car next-list)))
          (create-task-rec elems target (cdr next-list) result)
          (create-task-rec elems target (cdr next-list)
                           (append result
                                   (list (list (append elems (list (car next-list)))
                                               next-list)))))))

(define (create-task elems target next-list)
  (create-task-rec elems target next-list (list)))

(define (dfs result task target)
  (if (= 0 (length task)) result
      (let* ([current-task (car task)]
             [new-task (create-task (car current-task)
                                     target
                                     (cadr current-task))]
             [result (if (= (foldl + 0 (car current-task)) target)
                         (append result (list (car current-task)))
                         result)]
             [task (append new-task (cdr task))])
        (dfs result task target))))

(define (start-dfs lst target) (dfs (list) (create-task (list) target lst) target))

(define/contract (combination-sum candidates target)
  (-> (listof exact-integer?) exact-integer? (listof (listof exact-integer?)))
　(start-dfs candidates target))
```