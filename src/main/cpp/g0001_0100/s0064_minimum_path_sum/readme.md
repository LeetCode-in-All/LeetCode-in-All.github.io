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

```cpp
#include <vector>
#include <algorithm>

class Solution {
public:
    int minPathSum(std::vector<std::vector<int>>& grid) {
        if (grid.size() == 1 && grid[0].size() == 1) {
            return grid[0][0];
        }

        int m = grid.size();
        int n = grid[0].size();
        std::vector<std::vector<int>> dm(m, std::vector<int>(n, 0));
        int s = 0;

        // Initialize the last column
        for (int r = m - 1; r >= 0; --r) {
            dm[r][n - 1] = grid[r][n - 1] + s;
            s += grid[r][n - 1];
        }

        s = 0;
        // Initialize the last row
        for (int c = n - 1; c >= 0; --c) {
            dm[m - 1][c] = grid[m - 1][c] + s;
            s += grid[m - 1][c];
        }

        return recur(grid, dm, 0, 0);
    }

private:
    int recur(std::vector<std::vector<int>>& grid, std::vector<std::vector<int>>& dm, int r, int c) {
        int m = grid.size();
        int n = grid[0].size();
        if (dm[r][c] == 0 && r != m - 1 && c != n - 1) {
            dm[r][c] = grid[r][c] + std::min(recur(grid, dm, r + 1, c), recur(grid, dm, r, c + 1));
        }
        return dm[r][c];
    }
};
```