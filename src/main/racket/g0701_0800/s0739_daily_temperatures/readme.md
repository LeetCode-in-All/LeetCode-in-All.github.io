[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 739\. Daily Temperatures

Medium

Given an array of integers `temperatures` represents the daily temperatures, return _an array_ `answer` _such that_ `answer[i]` _is the number of days you have to wait after the_ <code>i<sup>th</sup></code> _day to get a warmer temperature_. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

**Example 1:**

**Input:** temperatures = [73,74,75,71,69,72,76,73]

**Output:** [1,1,4,2,1,1,0,0]

**Example 2:**

**Input:** temperatures = [30,40,50,60]

**Output:** [1,1,1,0]

**Example 3:**

**Input:** temperatures = [30,60,90]

**Output:** [1,1,0]

**Constraints:**

*   <code>1 <= temperatures.length <= 10<sup>5</sup></code>
*   `30 <= temperatures[i] <= 100`

## Solution

```racket
(define/contract (daily-temperatures temp)
    (-> (listof exact-integer?) (listof exact-integer?))
    (let make-answer
        ([i 0] [temp-rev (reverse temp)] [higher null] [answer null])
        (match temp-rev
            [(cons t temp-rev) (let* (
                [higher
                    (let eliminate<=t ([higher higher]) (match higher
                        [(cons (cons t1 _) higher) #:when (>= t t1) (eliminate<=t higher)]
                        [_ higher]))]
                [a (if (null? higher) 0 (- i (cdar higher)))] )
                (make-answer (add1 i) temp-rev (cons (cons t i) higher) (cons a answer)))]
            [(list) answer])))
```