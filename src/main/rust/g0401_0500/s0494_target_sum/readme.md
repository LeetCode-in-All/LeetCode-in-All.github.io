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

**Explanation:** There are 5 ways to assign symbols to make the sum of nums be target 3. 

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

```rust
impl Solution {
    pub fn find_target_sum_ways(nums: Vec<i32>, s: i32) -> i32 {
        let mut sum: i32 = nums.iter().sum();
        let s = s.abs();
        
        // Invalid cases
        if s > sum || (sum + s) % 2 != 0 {
            return 0;
        }

        let target = (sum + s) / 2;
        let n = nums.len();

        // dp[i] represents the number of ways to form sum i
        let mut dp = vec![vec![0; n + 1]; (target + 1) as usize];
        dp[0][0] = 1;

        // Handle empty knapsack condition
        for i in 0..n {
            if nums[i] == 0 {
                dp[0][i + 1] = dp[0][i] * 2;
            } else {
                dp[0][i + 1] = dp[0][i];
            }
        }

        // Fill the dp table
        for i in 1..=target {
            for j in 0..n {
                dp[i as usize][j + 1] += dp[i as usize][j];
                if nums[j] <= i {
                    dp[i as usize][j + 1] += dp[(i - nums[j]) as usize][j];
                }
            }
        }

        dp[target as usize][n]
    }
}
```