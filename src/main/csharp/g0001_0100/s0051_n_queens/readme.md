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

```csharp
public class Solution {
    public IList<IList<string>> SolveNQueens(int n) {
        return this.Backtrack(n, 0, (x, y) => false).ToList();
    }

    private IEnumerable<IList<string>> Backtrack(int boardSize, int y, Func<int, int, bool> check) {
        for (int x = 0; x < boardSize; x++) {
            if (check(x, y)) {
                continue;
            }
            string currentLine = $"{new string('.', x)}Q{new string('.', boardSize - x - 1)}";
            if (y == boardSize - 1) {
                yield return new List<string> { currentLine };
                continue;
            }
            var results = this.Backtrack(boardSize, y + 1, (xx, yy) =>
                check(xx, yy) ||
                (xx == x) ||
                (yy == (y - x) + xx) ||
                (yy == (x + y) - xx)
            );
            foreach (var result in results) {
                result.Add(currentLine);
                yield return result;
            }
        }
    }
}
```