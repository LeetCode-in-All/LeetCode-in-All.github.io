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

```rust
impl Solution {
    pub fn coin_change(coins: Vec<i32>, amount: i32) -> i32 {
        let mut dp = vec![0; (amount + 1) as usize];
        dp[0] = 1;  // Base case: one way to make 0 amount (using no coins)

        for &coin in &coins {
            for i in coin..=amount {
                let prev = dp[(i - coin) as usize];
                if prev > 0 {
                    if dp[i as usize] == 0 {
                        dp[i as usize] = prev + 1;
                    } else {
                        dp[i as usize] = dp[i as usize].min(prev + 1);
                    }
                }
            }
        }
        
        // If the dp[amount] is still 0, it means no solution was found
        if dp[amount as usize] == 0 {
            -1
        } else {
            dp[amount as usize] - 1
        }
    }
}
```