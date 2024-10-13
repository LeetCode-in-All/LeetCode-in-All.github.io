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

```dart
class Solution {
  List<List<String>> solveNQueens(int n) {
    final List<List<String>> board = List.generate(n, (_) => List<String>.filled(n, '.'));
    final List<List<String>> ans = [];
    backtrack(board, ans, 0, 0, n);
    return ans;
  }

  bool isSafe(List<List<String>> board, int row, int col) {
    for (int i = 0; i < row; i++) {
      if (board[i][col] == 'Q') {
        return false;
      }
    }

    for (int i = row, j = col; i >= 0 && j >= 0; i--, j--) {
      if (board[i][j] == 'Q') {
        return false;
      }
    }

    for (int i = row, j = col; i >= 0 && j < board.length; i--, j++) {
      if (board[i][j] == 'Q') {
        return false;
      }
    }

    return true;
  }

  void backtrack(List<List<String>> board, List<List<String>> ans, int row, int col, int queens) {
    if (row == queens) {
      ans.add(convert(board));
      return;
    }

    for (int col = 0; col < board.length; col++) {
      if (isSafe(board, row, col)) {
        board[row][col] = 'Q';
        backtrack(board, ans, row + 1, col, queens);
        board[row][col] = '.';
      }
    }
  }

  List<String> convert(List<List<String>> board) {
    final List<String> ans = [];
    for (int i = 0; i < board.length; i++) {
      final row = board[i].join('');
      ans.add(row);
    }

    return ans;
  }
}
```