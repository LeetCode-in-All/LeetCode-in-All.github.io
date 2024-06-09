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

```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        pos = [False] * (n + 2 * n - 1 + 2 * n - 1)
        pos2 = [0] * n
        ans = []
        self.helper(n, 0, pos, pos2, ans)
        return ans

    def helper(self, n: int, row: int, pos: List[bool], pos2: List[int], ans: List[List[str]]):
        if row == n:
            self.construct(n, pos2, ans)
            return
        for i in range(n):
            index = n + 2 * n - 1 + n - 1 + i - row
            if pos[i] or pos[n + i + row] or pos[index]:
                continue
            pos[i] = True
            pos[n + i + row] = True
            pos[index] = True
            pos2[row] = i
            self.helper(n, row + 1, pos, pos2, ans)
            pos[i] = False
            pos[n + i + row] = False
            pos[index] = False

    def construct(self, n: int, pos: list[int], ans: list[list[str]]):
        sol = []
        for r in range(n):
            queenRow = ['.'] * n
            queenRow[pos[r]] = 'Q'
            sol.append(''.join(queenRow))
        ans.append(sol)
```