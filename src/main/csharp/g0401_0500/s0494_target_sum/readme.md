[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 494\. Target Sum

Medium

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

*   For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

**Example 1:**

**Input:** nums = [1,1,1,1,1], target = 3

**Output:** 5

**Explanation:**

    There are 5 ways to assign symbols to make the sum of nums be target 3.
    -1 + 1 + 1 + 1 + 1 = 3
    +1 - 1 + 1 + 1 + 1 = 3
    +1 + 1 - 1 + 1 + 1 = 3
    +1 + 1 + 1 - 1 + 1 = 3
    +1 + 1 + 1 + 1 - 1 = 3 

**Example 2:**

**Input:** nums = [1], target = 1

**Output:** 1 

**Constraints:**

*   `1 <= nums.length <= 20`
*   `0 <= nums[i] <= 1000`
*   `0 <= sum(nums[i]) <= 1000`
*   `-1000 <= target <= 1000`

## Solution

```csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int FindTargetSumWays(int[] nums, int s) {
        int sum = 0;
        s = Math.Abs(s);
        foreach (int num in nums) {
            sum += num;
        }
        // Invalid s, just return 0
        if (s > sum || (sum + s) % 2 != 0) {
            return 0;
        }
        int[][] dp = new int[(sum + s) / 2 + 1][];
        for (int i = 0; i < dp.Length; i++) {
            dp[i] = new int[nums.Length + 1];
        }
        dp[0][0] = 1;
        // empty knapsack must be processed specially
        for (int i = 0; i < nums.Length; i++) {
            if (nums[i] == 0) {
                dp[0][i + 1] = dp[0][i] * 2;
            } else {
                dp[0][i + 1] = dp[0][i];
            }
        }
        for (int i = 1; i < dp.Length; i++) {
            for (int j = 0; j < nums.Length; j++) {
                dp[i][j + 1] += dp[i][j];
                if (nums[j] <= i) {
                    dp[i][j + 1] += dp[i - nums[j]][j];
                }
            }
        }
        return dp[(sum + s) / 2][nums.Length];
    }
}
```