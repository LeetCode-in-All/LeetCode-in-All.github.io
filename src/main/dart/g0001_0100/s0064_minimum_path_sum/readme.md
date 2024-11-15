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

```dart
class Solution {
  int minPathSum(List<List<int>> grid) {
    int m = grid.length;
    int n = grid[0].length;

    List<int> pathSum = List.filled(n, 100000);
    pathSum[0] = 0;

    for (int y = 0; y < m; y++) {
      for (int x = 0; x < n; x++) {
        pathSum[x] =
            (x > 0 ? min(pathSum[x], pathSum[x - 1]) : pathSum[x]) + grid[y][x];
      }
    }
    return pathSum[n - 1];
  }
}

int min(int a, int b) {
  if (a < b) {
    return a;
  }
  return b;
}
```