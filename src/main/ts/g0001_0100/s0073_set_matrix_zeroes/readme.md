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

```typescript
/*
 Do not return anything, modify matrix in-place instead.
 */
function setZeroes(matrix: number[][]): void { //NOSONAR
    const cols: number[] = []
    const rows: number[] = []
    for (let i = 0; i < matrix.length; i++) {
        for (let j = 0; j < matrix[i].length; j++) {
            if (matrix[i][j] === 0) {
                if (!rows.includes(i)) rows.push(i)
                if (!cols.includes(j)) cols.push(j)
            }
        }
    }
    for (const row of matrix) {
        for (const col of cols) {
            row[col] = 0
        }
    }
    for (let j = 0; j < rows.length; j++) {
        for (let i = 0; i < matrix[j].length; i++) {
            matrix[rows[j]][i] = 0
        }
    }
}

export { setZeroes }
```