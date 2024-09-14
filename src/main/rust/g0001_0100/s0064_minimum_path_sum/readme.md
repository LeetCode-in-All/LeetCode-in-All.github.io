[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 64\. Minimum Path Sum

Medium

Given a `m x n` `grid` filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

**Input:** grid = \[\[1,3,1],[1,5,1],[4,2,1]]

**Output:** 7

**Explanation:** Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.

**Example 2:**

**Input:** grid = \[\[1,2,3],[4,5,6]]

**Output:** 12

**Constraints:**

*   `m == grid.length`
*   `n == grid[i].length`
*   `1 <= m, n <= 200`
*   `0 <= grid[i][j] <= 100`

## Solution

```rust
impl Solution {
    pub fn min_path_sum(grid: Vec<Vec<i32>>) -> i32 {
        let (w, h) = (grid.len(), grid[0].len());
        let mut dp = vec![vec![0; h]; w];
        
        for i in 0..w {
            for j in 0..h {
                if i == 0 && j == 0 {
                    dp[i][j] = grid[i][j];
                } else if j == 0 {
                    dp[i][j] = grid[i][j] + dp[i-1][j];
                } else if i == 0 {
                    dp[i][j] = grid[i][j] + dp[i][j-1];
                } else {
                    dp[i][j] = grid[i][j] + std::cmp::min(dp[i-1][j], dp[i][j-1]);
                }
            }
        }

        dp[w-1][h-1]
    }
}
```