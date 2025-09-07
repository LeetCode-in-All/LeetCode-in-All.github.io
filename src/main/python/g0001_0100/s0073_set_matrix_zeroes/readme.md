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

To solve this task using Python with a `Solution` class, you can follow these steps:

1. Define a class named `Solution`.
2. Inside the class, define a method named `setZeroes` that takes `matrix` as an input parameter.
3. Implement the logic to set entire rows and columns to zeros if any element in the row or column is zero.
4. Use two boolean arrays `rows` and `cols` to keep track of which rows and columns need to be zeroed out.
5. Iterate through the matrix and update the corresponding elements in the `rows` and `cols` arrays if any zero is encountered.
6. Iterate through the matrix again and set the entire row to zeros if the corresponding `rows[i]` is True, and set the entire column to zeros if the corresponding `cols[j]` is True.

Here's the implementation:

```python
class Solution:
    def setZeroes(self, matrix):
        """
        Do not return anything, modify matrix in-place instead.
        """
        m, n = len(matrix), len(matrix[0])
        rows, cols = [False] * m, [False] * n
        
        # Mark which rows and columns contain zeros
        for i in range(m):
            for j in range(n):
                if matrix[i][j] == 0:
                    rows[i] = True
                    cols[j] = True
        
        # Set entire rows and columns to zeros
        for i in range(m):
            for j in range(n):
                if rows[i] or cols[j]:
                    matrix[i][j] = 0

# Example usage:
solution = Solution()
matrix1 = \[\[1,1,1],[1,0,1],[1,1,1]]
solution.setZeroes(matrix1)
print(matrix1)  # Output: [[1,0,1],[0,0,0],[1,0,1]] 

matrix2 = \[\[0,1,2,0],[3,4,5,2],[1,3,1,5]]
solution.setZeroes(matrix2)
print(matrix2)  # Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

This solution has a time complexity of O(m * n), where m is the number of rows and n is the number of columns in the matrix. It modifies the matrix in-place, fulfilling the requirement of the task.

## Solution

```python
from typing import List

class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        m = len(matrix)
        n = len(matrix[0])
        row0 = False
        col0 = False

        # Check if 0th column needs to be marked all 0s in future
        for i in range(m):
            if matrix[i][0] == 0:
                col0 = True
                break

        # Check if 0th row needs to be marked all 0s in future
        for j in range(n):
            if matrix[0][j] == 0:
                row0 = True
                break

        # Store the signals in 0th row and column
        for i in range(1, m):
            for j in range(1, n):
                if matrix[i][j] == 0:
                    matrix[i][0] = 0
                    matrix[0][j] = 0

        # Mark 0 for all cells based on signal from 0th row and 0th column
        for i in range(1, m):
            for j in range(1, n):
                if matrix[i][0] == 0 or matrix[0][j] == 0:
                    matrix[i][j] = 0

        # Set 0th column
        if col0:
            for i in range(m):
                matrix[i][0] = 0

        # Set 0th row
        if row0:
            for j in range(n):
                matrix[0][j] = 0
```