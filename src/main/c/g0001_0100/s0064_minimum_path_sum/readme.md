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

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

int recur(int** grid, int** dm, int r, int c, int rows, int cols) {
    if (dm[r][c] == 0 && r != rows - 1 && c != cols - 1) {
        dm[r][c] = grid[r][c] + (recur(grid, dm, r + 1, c, rows, cols) < recur(grid, dm, r, c + 1, rows, cols) 
                                 ? recur(grid, dm, r + 1, c, rows, cols) 
                                 : recur(grid, dm, r, c + 1, rows, cols));
    }
    return dm[r][c];
}

int minPathSum(int** grid, int gridSize, int* gridColSize) {
    if (gridSize == 1 && gridColSize[0] == 1) {
        return grid[0][0];
    }

    int rows = gridSize;
    int cols = gridColSize[0];
    int** dm = (int**)malloc(rows * sizeof(int*));
    for (int i = 0; i < rows; i++) {
        dm[i] = (int*)malloc(cols * sizeof(int));
        for (int j = 0; j < cols; j++) {
            dm[i][j] = 0; // Initialize to 0
        }
    }

    int s = 0;
    for (int r = rows - 1; r >= 0; r--) {
        dm[r][cols - 1] = grid[r][cols - 1] + s;
        s += grid[r][cols - 1];
    }

    s = 0;
    for (int c = cols - 1; c >= 0; c--) {
        dm[rows - 1][c] = grid[rows - 1][c] + s;
        s += grid[rows - 1][c];
    }

    int result = recur(grid, dm, 0, 0, rows, cols);

    // Free allocated memory
    for (int i = 0; i < rows; i++) {
        free(dm[i]);
    }
    free(dm);

    return result;
}
```