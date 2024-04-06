[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 200\. Number of Islands

Medium

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

**Input:**

    grid = [
      ["1","1","1","1","0"],
      ["1","1","0","1","0"],
      ["1","1","0","0","0"],
      ["0","0","0","0","0"]
    ]

**Output:** 1 

**Example 2:**

**Input:**

    grid = [
      ["1","1","0","0","0"],
      ["1","1","0","0","0"],
      ["0","0","1","0","0"],
      ["0","0","0","1","1"]
    ]

**Output:** 3 

**Constraints:**

*   `m == grid.length`
*   `n == grid[i].length`
*   `1 <= m, n <= 300`
*   `grid[i][j]` is `'0'` or `'1'`.

## Solution

```scala
object Solution {
    def numIslands(grid: Array[Array[Char]]): Int = {
        var islands = 0

        def dfs(x: Int, y: Int): Unit = {
            if (x < 0 || x >= grid.length || y < 0 || y >= grid(0).length || grid(x)(y) != '1') {
                return
            }
            grid(x)(y) = 'x'
            dfs(x + 1, y)
            dfs(x - 1, y)
            dfs(x, y + 1)
            dfs(x, y - 1)
        }

        if (grid != null && grid.length > 0 && grid(0).length > 0) {
            for (i <- grid.indices) {
                for (j <- grid(0).indices) {
                    if (grid(i)(j) == '1') {
                        dfs(i, j)
                        islands += 1
                    }
                }
            }
        }
        islands
    }
}
```