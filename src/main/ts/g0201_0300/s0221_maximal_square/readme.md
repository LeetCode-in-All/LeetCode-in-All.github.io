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

```typescript
function maximalSquare(matrix: string[][]): number {
    const m = matrix.length
    if (m === 0) {
        return 0
    }
    const n = matrix[0].length
    if (n === 0) {
        return 0
    }
    const dp: number[][] = new Array(m + 1).fill(0).map(() => new Array(n + 1).fill(0))
    let max = 0
    for (let i = 0; i < m; i++) {
        for (let j = 0; j < n; j++) {
            if (matrix[i][j] === '1') {
                // 1 + minimum from cell above, cell to the left, cell diagonal upper-left
                const next = 1 + Math.min(dp[i][j], Math.min(dp[i + 1][j], dp[i][j + 1]))
                // keep track of the maximum value seen
                if (next > max) {
                    max = next
                }
                dp[i + 1][j + 1] = next
            }
        }
    }
    return max * max
}

export { maximalSquare }
```