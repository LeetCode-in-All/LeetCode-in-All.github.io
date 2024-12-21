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

```javascript
/**
 * @param {character[][]} mArr
 * @return {number}
 */
var maximalSquare = function(mArr) {
    if (mArr.length === 0 || mArr[0].length === 0) return 0

    let maxLen = 0
    let rows = mArr.length
    let cols = mArr[0].length
    let dpArr = Array.from({ length: rows }, () => new Array(cols).fill(0))

    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < cols; j++) {
            if (mArr[i][j] === '0') continue
            dpArr[i][j] = 1
            if (i > 0 && j > 0) {
                dpArr[i][j] = Math.min(
                    dpArr[i - 1][j],
                    dpArr[i][j - 1],
                    dpArr[i - 1][j - 1]
                ) + 1
            }
            maxLen = Math.max(maxLen, dpArr[i][j])
        }
    }
    return maxLen * maxLen
};

export { maximalSquare }
```