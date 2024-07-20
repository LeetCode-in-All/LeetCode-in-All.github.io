[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 70\. Climbing Stairs

Easy

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**

**Input:** n = 2

**Output:** 2

**Explanation:** There are two ways to climb to the top. 1. 1 step + 1 step 2. 2 steps 

**Example 2:**

**Input:** n = 3

**Output:** 3

**Explanation:** There are three ways to climb to the top. 1. 1 step + 1 step + 1 step 2. 1 step + 2 steps 3. 2 steps + 1 step 

**Constraints:**

*   `1 <= n <= 45`

## Solution

```csharp
public class Solution {
    public int ClimbStairs(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 1;
        for (int i = 0; i < dp.Length; i++) {
            if (i + 1 < dp.Length) {
                dp[i + 1] += dp[i];
            }
            if (i + 2 < dp.Length) {
                dp[i + 2] += dp[i];
            }
        }
        return dp[dp.Length - 1];
    }
}
```