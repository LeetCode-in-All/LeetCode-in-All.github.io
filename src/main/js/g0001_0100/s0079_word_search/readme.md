[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 79\. Word Search

Medium

Given an `m x n` grid of characters `board` and a string `word`, return `true` _if_ `word` _exists in the grid_.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

**Input:** board = \[\["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"

**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

**Input:** board = \[\["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"

**Output:** true

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

**Input:** board = \[\["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"

**Output:** false

**Constraints:**

*   `m == board.length`
*   `n = board[i].length`
*   `1 <= m, n <= 6`
*   `1 <= word.length <= 15`
*   `board` and `word` consists of only lowercase and uppercase English letters.

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?

## Solution

```javascript
/**
 * @param {character[][]} board
 * @param {string} word
 * @return {boolean}
 */
var exist = function (board, word) {
    let visited = Array.from({ length: board.length }, () => Array(board[0].length).fill(0)),
        m = board.length, n = board[0].length, isMatch = false
    const dfs = (i, j, match) => {
        visited[i][j] = 1
        if (match == word.length) {
            isMatch = true
            return
        }
        let x = [1, -1, 0, 0], y = [0, 0, 1, -1]
        for (let k = 0; k < 4; k++) {
            let xx = x[k] + i, yy = y[k] + j
            if (xx >= 0 && yy >= 0 && xx < m && yy < n && visited[xx][yy] != 1 && board[xx][yy] == word[match]) {
                dfs(xx, yy, match + 1)
                visited[xx][yy] = 0
            }
        }
    }
    for (let i = 0; i < board.length; i++) {
        for (let j = 0; j < board[0].length; j++) {
            if (board[i][j] == word[0]) {
                dfs(i, j, 1)
                if (isMatch) {
                    return true
                }
                visited = Array.from({ length: board.length }, () => Array(board[0].length).fill(0))

            }
        }
    }
    return isMatch
};

export { exist }
```