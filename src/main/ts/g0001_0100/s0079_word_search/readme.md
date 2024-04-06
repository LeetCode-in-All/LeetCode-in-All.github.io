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

```typescript
function exist(board: string[][], word: string): boolean {
    if (word.length === 0) return false
    let ret = false
    const marks = makeArray(board)
    for (let i = 0; i < board.length; i++) {
        for (let j = 0; j < board[i].length; j++) {
            if (board[i][j] !== word.charAt(0)) continue
            if (loop(marks, board, i, j, word, 0)) return true
        }
    }

    return ret
}

function makeArray(board: string[][]) {
    const arr = []
    for (let i = 0; i < board.length; i++) {
        arr[i] = []
        for (let j = 0; j < board[i].length; j++) {
            arr[i][j] = false
        }
    }
    return arr
}

function loop(marks: boolean[][], board: string[][], i: number, j: number, word: string, index: number): boolean {
    if (i < 0 || j < 0 || i >= board.length || j >= board[i].length || marks[i][j]) {
        return false
    }

    if (board[i][j] !== word.charAt(index)) {
        return false
    } else if (index === word.length - 1) {
        return true
    }

    marks[i][j] = true
    index++

    let r = loop(marks, board, i - 1, j, word, index)
    if (r) return true

    r = loop(marks, board, i + 1, j, word, index)
    if (r) return true

    r = loop(marks, board, i, j - 1, word, index)
    if (r) return true

    r = loop(marks, board, i, j + 1, word, index)
    if (r) return true

    marks[i][j] = false
    return false
}

export { exist }
```