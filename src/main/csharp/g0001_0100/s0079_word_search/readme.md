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

```csharp
public class Solution {
    public bool Exist(char[][] board, string word) {
        for (int i = 0; i < board.Length; i++) {
            for (int j = 0; j < board[0].Length; j++) {
                char ch = word[0];
                if (board[i][j] == ch) {
                    if (helper(i, j, board, word, 1)) {
                        return true;
                    }
                }
            }
        }
        return false;
    }

    private bool helper(int r, int c, char[][] board, string word, int count) {
        if (count == word.Length) {
            return true;
        }
        char currChar = board[r][c];
        board[r][c] = '!';
        char nextChar = word[count];
        if (r > 0 && board[r - 1][c] == nextChar) {
            if (helper(r - 1, c, board, word, count + 1)) return true;
        }
        if (r < board.Length - 1 && board[r + 1][c] == nextChar) {
            if (helper(r + 1, c, board, word, count + 1)) return true;
        }
        if (c > 0 && board[r][c - 1] == nextChar) {
            if (helper(r, c - 1, board, word, count + 1)) return true;
        }
        if (c < board[0].Length - 1 && board[r][c + 1] == nextChar) {
            if (helper(r, c + 1, board, word, count + 1)) return true;
        }
        board[r][c] = currChar;
        return false;
    }
}
```