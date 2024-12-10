[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 51\. N-Queens

Hard

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _all distinct solutions to the **n-queens puzzle**_. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

**Input:** n = 4

**Output:** [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]

**Explanation:** There exist two distinct solutions to the 4-queens puzzle as shown above

**Example 2:**

**Input:** n = 1

**Output:** [["Q"]]

**Constraints:**

*   `1 <= n <= 9`

## Solution

```javascript
/**
 * @param {number} n
 * @return {string[][]}
 */
var solveNQueens = function(n) {
    const board = Array.from({ length: n }, () => Array(n).fill('.'))
    const res = []
    const leftRow = new Array(n).fill(0)
    const upperDiagonal = new Array(2 * n - 1).fill(0)
    const lowerDiagonal = new Array(2 * n - 1).fill(0)

    const solve = (col) => {
        if (col === n) {
            res.push(construct(board))
            return
        }
        for (let row = 0; row < n; row++) {
            if (
                leftRow[row] === 0 &&
                lowerDiagonal[row + col] === 0 &&
                upperDiagonal[n - 1 + col - row] === 0
            ) {
                board[row][col] = 'Q'
                leftRow[row] = 1
                lowerDiagonal[row + col] = 1
                upperDiagonal[n - 1 + col - row] = 1
                solve(col + 1)
                board[row][col] = '.'
                leftRow[row] = 0
                lowerDiagonal[row + col] = 0
                upperDiagonal[n - 1 + col - row] = 0
            }
        }
    }

    const construct = (board) => {
        return board.map(row => row.join(''))
    }

    solve(0)
    return res
}

export { solveNQueens }
```