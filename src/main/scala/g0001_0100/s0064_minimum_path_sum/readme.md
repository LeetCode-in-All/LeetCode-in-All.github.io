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

```scala
object Solution {
    def minPathSum(grid: Array[Array[Int]]): Int = {
        val numRows = grid.length
        val numCols = grid(0).length
        val dp = Array.ofDim[Int](numRows, numCols)

        for (r <- numRows - 1 to 0 by -1) {
            for (c <- numCols - 1 to 0 by -1) {
                if (r == numRows - 1 && c == numCols - 1) {
                    dp(r)(c) = grid(r)(c)
                } else if (r == numRows - 1) {
                    dp(r)(c) = grid(r)(c) + dp(r)(c + 1)
                } else if (c == numCols - 1) {
                    dp(r)(c) = grid(r)(c) + dp(r + 1)(c)
                } else {
                    dp(r)(c) = grid(r)(c) + Math.min(dp(r + 1)(c), dp(r)(c + 1))
                }
            }
        }
        dp(0)(0)
    }
}
```