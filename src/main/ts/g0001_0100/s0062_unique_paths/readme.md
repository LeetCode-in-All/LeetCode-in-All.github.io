[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 62\. Unique Paths

Medium

A robot is located at the top-left corner of a `m x n` grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

**Input:** m = 3, n = 7

**Output:** 28 

**Example 2:**

**Input:** m = 3, n = 2

**Output:** 3

**Explanation:**

    From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
    1. Right -> Down -> Down
    2. Down -> Down -> Right
    3. Down -> Right -> Down 

**Example 3:**

**Input:** m = 7, n = 3

**Output:** 28 

**Example 4:**

**Input:** m = 3, n = 3

**Output:** 6 

**Constraints:**

*   `1 <= m, n <= 100`
*   It's guaranteed that the answer will be less than or equal to <code>2 * 10<sup>9</sup></code>.

## Solution

```typescript
function uniquePaths(m: number, n: number): number {
    let aboveRow = Array(n).fill(1)
    for (let row = 1; row < m; row++) {
        let currentRow = Array(n).fill(1)
        for (let col = 1; col < n; col++) {
            currentRow[col] = currentRow[col - 1] + aboveRow[col]
        }
        aboveRow = currentRow
    }
    return aboveRow[n - 1]
}

export { uniquePaths }
```