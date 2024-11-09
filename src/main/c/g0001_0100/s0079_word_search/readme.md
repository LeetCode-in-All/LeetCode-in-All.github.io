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

```c
bool dfsb(char **board, int mrow, int mcol, char *word, int crow, int ccol) {
    // This means we are done with search
    if (word[0] == '\0') {
        return true;
    }

    // Out of bound check; search ends in this path
    if (crow < 0 || ccol < 0 || crow >= mrow || ccol >= mcol) {
        return false;
    }

    // Not found; search ends
    if (board[crow][ccol] != word[0]) {
        return false;
    }

    // Mark the cell as visited
    board[crow][ccol] = '.';

    // Check adjacent cells
    if (dfsb(board, mrow, mcol, word + 1, crow, ccol + 1)) return true; // Right
    if (dfsb(board, mrow, mcol, word + 1, crow, ccol - 1)) return true; // Left
    if (dfsb(board, mrow, mcol, word + 1, crow - 1, ccol)) return true; // Up
    if (dfsb(board, mrow, mcol, word + 1, crow + 1, ccol)) return true; // Down

    // Undo marking if no match found
    board[crow][ccol] = word[0];
    return false;
}

bool exist(char **board, int num_rows, int *num_cols, char *word) {
    for (int row = 0; row < num_rows; ++row) {
        for (int col = 0; col < *num_cols; ++col) {
            if (dfsb(board, num_rows, *num_cols, word, row, col)) {
                return true;
            }
        }
    }
    return false;
}
```