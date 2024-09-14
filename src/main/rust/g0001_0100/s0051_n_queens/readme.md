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

```rust
impl Solution {
    pub fn solve_n_queens(n: i32) -> Vec<Vec<String>> {
        let mut pos = vec![false; n as usize + 2 * n as usize - 1 + 2 * n as usize - 1];
        let mut pos2 = vec![0; n as usize];
        let mut ans = Vec::new();
        Solution::helper(n as usize, 0, &mut pos, &mut pos2, &mut ans);
        ans
    }

    fn helper(
        n: usize,
        row: usize,
        pos: &mut Vec<bool>,
        pos2: &mut Vec<usize>,
        ans: &mut Vec<Vec<String>>,
    ) {
        if row == n {
            Solution::construct(n, pos2, ans);
            return;
        }

        for i in 0..n {
            let index = n + 2 * n - 1 + n - 1 + i - row;
            if pos[i] || pos[n + i + row] || pos[index] {
                continue;
            }

            pos[i] = true;
            pos[n + i + row] = true;
            pos[index] = true;
            pos2[row] = i;

            Solution::helper(n, row + 1, pos, pos2, ans);

            pos[i] = false;
            pos[n + i + row] = false;
            pos[index] = false;
        }
    }

    fn construct(n: usize, pos2: &Vec<usize>, ans: &mut Vec<Vec<String>>) {
        let mut sol = Vec::new();
        for r in 0..n {
            let mut queen_row = vec!['.'; n];
            queen_row[pos2[r]] = 'Q';
            sol.push(queen_row.into_iter().collect());
        }
        ans.push(sol);
    }
}
```