[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 322\. Coin Change

Medium

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return _the fewest number of coins that you need to make up that amount_. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

**Example 1:**

**Input:** coins = [1,2,5], amount = 11

**Output:** 3

**Explanation:** 11 = 5 + 5 + 1

**Example 2:**

**Input:** coins = [2], amount = 3

**Output:** -1

**Example 3:**

**Input:** coins = [1], amount = 0

**Output:** 0

**Constraints:**

*   `1 <= coins.length <= 12`
*   <code>1 <= coins[i] <= 2<sup>31</sup> - 1</code>
*   <code>0 <= amount <= 10<sup>4</sup></code>

## Solution

```racket
(define/contract (coin-change coins amount)
  (-> (listof exact-integer?) exact-integer? exact-integer?)
  (let ([dp (make-vector (+ amount 1) 0)])
    (vector-set! dp 0 1)
    (for ([coin coins])
      (for ([i (in-range coin (+ amount 1))])
        (let ([prev (vector-ref dp (- i coin))])
          (when (> prev 0)
            (vector-set! dp i
                         (if (= (vector-ref dp i) 0)
                             (+ prev 1)
                             (min (vector-ref dp i) (+ prev 1))))))))
    (- (vector-ref dp amount) 1)))
```