[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 73\. Set Matrix Zeroes

Medium

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s, and return _the matrix_.

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

```scala
object Solution {
    @SuppressWarnings(Array("scala:S3776"))
    def setZeroes(matrix: Array[Array[Int]]): Unit = {
        val m = matrix.length
        val n = matrix(0).length
        var row0 = false
        var col0 = false

        // Check if the 0th column needs to be marked as all 0s in the future
        for (row <- matrix) {
            if (row(0) == 0) {
                col0 = true
            }
        }

        // Check if the 0th row needs to be marked as all 0s in the future
        for (i <- 0 until n) {
            if (matrix(0)(i) == 0) {
                row0 = true
            }
        }

        // Store the signals in the 0th row and column
        for (i <- 1 until m) {
            for (j <- 1 until n) {
                if (matrix(i)(j) == 0) {
                    matrix(i)(0) = 0
                    matrix(0)(j) = 0
                }
            }
        }

        // Mark 0 for all cells based on signals from the 0th row and 0th column
        for (i <- 1 until m) {
            for (j <- 1 until n) {
                if (matrix(i)(0) == 0 || matrix(0)(j) == 0) {
                    matrix(i)(j) = 0
                }
            }
        }

        // Set the 0th column
        for (i <- 0 until m) {
            if (col0) {
                matrix(i)(0) = 0
            }
        }

        // Set the 0th row
        for (i <- 0 until n) {
            if (row0) {
                matrix(0)(i) = 0
            }
        }
    }
}
```