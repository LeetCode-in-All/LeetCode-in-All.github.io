[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 48\. Rotate Image

Medium

You are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).

You have to rotate the image [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg)

**Input:** matrix = \[\[1,2,3],[4,5,6],[7,8,9]]

**Output:** [[7,4,1],[8,5,2],[9,6,3]]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg)

**Input:** matrix = \[\[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]

**Output:** [[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]

**Constraints:**

*   `n == matrix.length == matrix[i].length`
*   `1 <= n <= 20`
*   `-1000 <= matrix[i][j] <= 1000`

## Solution

```dart
class Solution {
  void rotate(List<List<int>> matrix) {
    int n = matrix.length;

    for (int i = 0; i < n ~/ 2; i++) {
      for (int j = i; j < n - i - 1; j++) {
        List<List<int>> pos = [
          [i, j],
          [j, n - 1 - i],
          [n - 1 - i, n - 1 - j],
          [n - 1 - j, i]
        ];

        int t = matrix[pos[0][0]][pos[0][1]];
        for (int k = 1; k < pos.length; k++) {
          int temp = matrix[pos[k][0]][pos[k][1]];
          matrix[pos[k][0]][pos[k][1]] = t;
          t = temp;
        }
        matrix[pos[0][0]][pos[0][1]] = t;
      }
    }
  }
}
```