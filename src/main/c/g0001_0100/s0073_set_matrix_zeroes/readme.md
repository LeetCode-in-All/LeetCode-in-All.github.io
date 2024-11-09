[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 73\. Set Matrix Zeroes

Medium

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

**Input:** matrix = \[\[1,1,1],[1,0,1],[1,1,1]]

**Output:** [[1,0,1],[0,0,0],[1,0,1]]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)

**Input:** matrix = \[\[0,1,2,0],[3,4,5,2],[1,3,1,5]]

**Output:** [[0,0,0,0],[0,4,5,0],[0,3,1,0]]

**Constraints:**

*   `m == matrix.length`
*   `n == matrix[0].length`
*   `1 <= m, n <= 200`
*   <code>-2<sup>31</sup> <= matrix[i][j] <= 2<sup>31</sup> - 1</code>

**Follow up:**

*   A straightforward solution using `O(mn)` space is probably a bad idea.
*   A simple improvement uses `O(m + n)` space, but still not the best solution.
*   Could you devise a constant space solution?

## Solution

```c
#include <stdio.h>
#include <stdlib.h>

void setZeroRow(int **matrix, int cols, int row) {
    for (int j = 0; j < cols; j++) {
        matrix[row][j] = 0;
    }
}

void setZeroCol(int **matrix, int rows, int col) {
    for (int i = 0; i < rows; i++) {
        matrix[i][col] = 0;
    }
}

void setZeroes(int** matrix, int matrixSize, int* matrixColSize) {
    int setFirstRow = 0, setFirstCol = 0;

    // Step 1: Determine which rows and columns to zero out
    for (int i = 0; i < matrixSize; i++) {
        for (int j = 0; j < *matrixColSize; j++) {
            if (matrix[i][j] == 0) {
                matrix[i][0] = 0;  // Mark the first column
                matrix[0][j] = 0;  // Mark the first row

                if (i == 0) setFirstRow = 1;  // Indicate first row needs to be zeroed
                if (j == 0) setFirstCol = 1;  // Indicate first column needs to be zeroed
            }
        }
    }

    // Step 2: Zero out cells based on marks in the first row and column
    for (int i = matrixSize - 1; i > 0; i--) {
        if (matrix[i][0] == 0) {
            setZeroRow(matrix, *matrixColSize, i);
        }
    }

    for (int j = *matrixColSize - 1; j > 0; j--) {
        if (matrix[0][j] == 0) {
            setZeroCol(matrix, matrixSize, j);
        }
    }

    // Step 3: Zero out the first row and column if needed
    if (setFirstRow) {
        setZeroRow(matrix, *matrixColSize, 0);
    }
    if (setFirstCol) {
        setZeroCol(matrix, matrixSize, 0);
    }
}
```