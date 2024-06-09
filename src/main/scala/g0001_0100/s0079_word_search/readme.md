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

```scala
object Solution {
    private val directions = Array(Array(-1, 0), Array(1, 0), Array(0, -1), Array(0, 1))
    private var numRows, numCols = 0

    def exist(board: Array[Array[Char]], word: String): Boolean = {
        if (board.length == 0) return false
        if (word.isEmpty) return true
        numRows = board.length
        numCols = board(0).length
        var result = false
        for (row <- 0 until numRows if !result) {
            for (col <- 0 until numCols if !result) {
                if (board(row)(col) == word(0)) {
                    result = backTracking(board, row, col, word, 0)
                }
            }
        }
        result
    }

    private def backTracking(board: Array[Array[Char]], row: Int, col: Int, word: String, index: Int): Boolean = {
        if (index >= word.length) return true
        if (row < 0 || row >= numRows || col < 0 || col >= numCols || board(row)(col) != word(index) || board(row)(col) == '0') {
            return false
        }
        val originalValue = board(row)(col)
        board(row)(col) = '0'
        var output = false
        for (dir <- directions if !output) {
            val newRow = row + dir(0)
            val newCol = col + dir(1)
            output = backTracking(board, newRow, newCol, word, index + 1)
        }
        board(row)(col) = originalValue
        output
    }
}
```