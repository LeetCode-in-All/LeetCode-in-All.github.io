[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 221\. Maximal Square

Medium

Given an `m x n` binary `matrix` filled with `0`'s and `1`'s, _find the largest square containing only_ `1`'s _and return its area_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/max1grid.jpg)

**Input:** matrix = \[\["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]

**Output:** 4

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/26/max2grid.jpg)

**Input:** matrix = \[\["0","1"],["1","0"]]

**Output:** 1

**Example 3:**

**Input:** matrix = \[\["0"]]

**Output:** 0

**Constraints:**

*   `m == matrix.length`
*   `n == matrix[i].length`
*   `1 <= m, n <= 300`
*   `matrix[i][j]` is `'0'` or `'1'`.

## Solution

```c
#include <stdio.h>
#include <stdlib.h>

int min(int a, int b) {
    return a < b ? a : b;
}

int min3(int a, int b, int c) {
    return min(a, min(b, c));
}

int maximalSquare(char** matrix, int matrixSize, int* matrixColSize) {
    if (matrixSize == 0 || matrixColSize[0] == 0) {
        return 0;
    }
    
    int m = matrixSize;
    int n = matrixColSize[0];
    
    // Create a dynamic programming (dp) array initialized to 0
    int** dp = (int**)malloc((m + 1) * sizeof(int*));
    for (int i = 0; i <= m; i++) {
        dp[i] = (int*)calloc(n + 1, sizeof(int));
    }
    
    int max = 0;
    
    // Fill the dp array based on the matrix values
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (matrix[i - 1][j - 1] == '1') {
                dp[i][j] = 1 + min3(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]);
                if (dp[i][j] > max) {
                    max = dp[i][j];
                }
            }
        }
    }
    
    // Free allocated memory for dp array
    for (int i = 0; i <= m; i++) {
        free(dp[i]);
    }
    free(dp);
    
    return max * max;
}
```