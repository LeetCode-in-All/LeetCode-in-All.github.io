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

```c
#include <stdio.h>
#include <limits.h>

int coinChange(int* coins, int coinsSize, int amount) {
    int* dp = (int*)malloc((amount + 1) * sizeof(int));

    // Initialize dp array, where dp[i] represents the minimum number of coins to make amount i.
    // Set dp[0] to 1 as the base case (1 represents that 0 coins are needed to make amount 0).
    dp[0] = 1;
    for (int i = 1; i <= amount; i++) {
        dp[i] = 0;
    }

    for (int c = 0; c < coinsSize; c++) {
        int coin = coins[c];
        for (int i = coin; i <= amount; i++) {
            int prev = dp[i - coin];
            if (prev > 0) {  // If it's possible to make amount (i - coin)
                if (dp[i] == 0) {
                    dp[i] = prev + 1;
                } else {
                    dp[i] = (dp[i] < prev + 1) ? dp[i] : prev + 1;
                }
            }
        }
    }

    int result = (dp[amount] > 0) ? dp[amount] - 1 : -1; // Subtract 1 to account for the base case offset

    free(dp); // Free allocated memory
    return result;
}
```