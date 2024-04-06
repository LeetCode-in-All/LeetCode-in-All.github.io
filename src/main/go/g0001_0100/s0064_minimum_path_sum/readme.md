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

```golang
func minPathSum(grid [][]int) int {
	if len(grid) == 1 && len(grid[0]) == 1 {
		return grid[0][0]
	}
	dm := make([][]int, len(grid))
	for i := range dm {
		dm[i] = make([]int, len(grid[0]))
	}
	sum := 0
	for r := len(grid) - 1; r >= 0; r-- {
		dm[r][len(grid[0])-1] = grid[r][len(grid[0])-1] + sum
		sum += grid[r][len(grid[0])-1]
	}
	sum = 0
	for c := len(grid[0]) - 1; c >= 0; c-- {
		dm[len(grid)-1][c] = grid[len(grid)-1][c] + sum
		sum += grid[len(grid)-1][c]
	}
	return recur(grid, dm, 0, 0)
}

func recur(grid [][]int, dm [][]int, r, c int) int {
	if dm[r][c] == 0 && r != len(grid)-1 && c != len(grid[0])-1 {
		dm[r][c] = grid[r][c] + min(recur(grid, dm, r+1, c), recur(grid, dm, r, c+1))
	}
	return dm[r][c]
}

func min(a, b int) int {
	if a < b {
		return a
	}
	return b
}
```