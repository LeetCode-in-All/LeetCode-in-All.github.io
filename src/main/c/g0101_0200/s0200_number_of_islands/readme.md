[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 200\. Number of Islands

Medium

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

**Input:** grid = [ 

["1","1","1","1","0"], 

["1","1","0","1","0"], 

["1","1","0","0","0"], 

["0","0","0","0","0"] 

]

**Output:** 1

**Example 2:**

**Input:** grid = [ 

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

```c
void DFS(int row, int col, int m, int n, char** grid) {
    if (row < 0 || row >= m || col < 0 || col >= n || grid[row][col] == '0') {
        return;
    }

    grid[row][col] = '0'; // Mark the current cell as visited

    // Visit the neighboring cells
    DFS(row + 1, col, m, n, grid);
    DFS(row - 1, col, m, n, grid);
    DFS(row, col + 1, m, n, grid);
    DFS(row, col - 1, m, n, grid);
}

int numIslands(char** grid, int gridSize, int* gridColSize) {
    if (gridSize == 0) {
        return 0;
    }

    int m = gridSize;  // ROW
    int n = *gridColSize; // COL
    int numIslands = 0;

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (grid[i][j] == '1') {  // grid[row][col]
                numIslands++;
                DFS(i, j, m, n, grid);
            }
        }
    }

    return numIslands;
}
```