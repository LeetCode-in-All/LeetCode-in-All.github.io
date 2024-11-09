[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 62\. Unique Paths

Medium

There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return _the number of possible unique paths that the robot can take to reach the bottom-right corner_.

The test cases are generated so that the answer will be less than or equal to <code>2 * 10<sup>9</sup></code>.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

**Input:** m = 3, n = 7

**Output:** 28

**Example 2:**

**Input:** m = 3, n = 2

**Output:** 3

**Explanation:** From the top-left corner, there are a total of 3 ways to reach the bottom-right corner: 

1. Right -> Down -> Down 

2. Down -> Down -> Right 

3. Down -> Right -> Down

**Constraints:**

*   `1 <= m, n <= 100`

## Solution

```c
#include <stdio.h>
#include <stdlib.h>

int uniquePaths(int m, int n) {
    // Step 1: Allocate a 2D array for dynamic programming
    int** dp = (int**)malloc(m * sizeof(int*));
    for (int i = 0; i < m; i++) {
        dp[i] = (int*)malloc(n * sizeof(int));
    }

    // Step 2: Initialize the first column
    for (int i = 0; i < m; i++) {
        dp[i][0] = 1;
    }

    // Step 3: Initialize the first row
    for (int j = 0; j < n; j++) {
        dp[0][j] = 1;
    }

    // Step 4: Fill the rest of the dp array
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }
    }

    // Step 5: Store the result
    int result = dp[m - 1][n - 1];

    // Step 6: Free allocated memory
    for (int i = 0; i < m; i++) {
        free(dp[i]);
    }
    free(dp);

    return result;
}
```