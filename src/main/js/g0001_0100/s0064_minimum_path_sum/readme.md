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

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function(grid) {
    const rows = grid.length
    const cols = grid[0].length

    // Handle the special case where grid has only one cell
    if (rows === 1 && cols === 1) {
        return grid[0][0]
    }

    // Create a 2D array for dynamic programming
    const dm = Array.from({ length: rows }, () => Array(cols).fill(0))

    // Initialize the last column
    let s = 0
    for (let r = rows - 1; r >= 0; r--) {
        dm[r][cols - 1] = grid[r][cols - 1] + s
        s += grid[r][cols - 1]
    }

    // Initialize the last row
    s = 0
    for (let c = cols - 1; c >= 0; c--) {
        dm[rows - 1][c] = grid[rows - 1][c] + s
        s += grid[rows - 1][c]
    }

    // Recursive helper function
    const recur = (r, c) => {
        if (
            dm[r][c] === 0 &&
            r !== rows - 1 &&
            c !== cols - 1
        ) {
            dm[r][c] =
                grid[r][c] +
                Math.min(
                    recur(r + 1, c),
                    recur(r, c + 1)
                )
        }
        return dm[r][c]
    }

    // Start recursion from the top-left corner
    return recur(0, 0)
};

export { minPathSum }
```