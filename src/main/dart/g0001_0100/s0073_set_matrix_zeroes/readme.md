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

```dart
class Solution {
  void setZeroes(List<List<int>> matrix) {
    int nRow = matrix.length;
    int nCol = matrix.first.length;
    bool fr = false;
    bool lr = false;
    bool fc = false;
    bool lc = false;

    for (int i = 0; i < nCol; i++) {
      if (matrix[0][i] == 0) {
        fr = true;
      }
      if (matrix[nRow - 1][i] == 0) {
        lr = true;
      }
    }

    for (int i = 0; i < nRow; i++) {
      if (matrix[i][0] == 0) {
        fc = true;
      }
      if (matrix[i][nCol - 1] == 0) {
        lc = true;
      }
    }

    for (int i = 1; i < nRow - 1; i++) {
      for (int j = 1; j < nCol - 1; j++) {
        if (matrix[i][j] == 0) {
          matrix[0][j] = 0;
          matrix[i][0] = 0;
        }
      }
    }

    for (int i = 1; i < nRow - 1; i++) {
      if (matrix[i][0] == 0 || matrix[i][nCol - 1] == 0) {
        for (int j = 0; j < nCol; j++) {
          matrix[i][j] = 0;
        }
      }
    }

    for (int i = 1; i < nCol - 1; i++) {
      if (matrix[0][i] == 0 || matrix[nRow - 1][i] == 0) {
        for (int j = 0; j < nRow; j++) {
          matrix[j][i] = 0;
        }
      }
    }


    if (fr) {
      for (int i = 0; i < nCol; i++) {
        matrix[0][i] = 0;
      }
    }
    if (lr) {
      for (int i = 0; i < nCol; i++) {
        matrix[nRow - 1][i] = 0;
      }
    }
    if (fc) {
      for (int i = 0; i < nRow; i++) {
        matrix[i][0] = 0;
      }
    }
    if (lc) {
      for (int i = 0; i < nRow; i++) {
        matrix[i][nCol - 1] = 0;
      }
    }
  }
}
```