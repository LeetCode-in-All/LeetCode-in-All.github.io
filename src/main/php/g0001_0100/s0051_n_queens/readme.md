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

```php
class Solution {
    /**
     * @param Integer $n
     * @return String[][]
     */
    public function solveNQueens($n) {
        $pos = array_fill(0, $n + 2 * $n - 1 + 2 * $n - 1, false);
        $pos2 = array_fill(0, $n, 0);
        $ans = array();
        $this->helper($n, 0, $pos, $pos2, $ans);
        return $ans;
    }

    private function helper($n, $row, &$pos, &$pos2, &$ans) {
        if ($row == $n) {
            $this->construct($n, $pos2, $ans);
            return;
        }
        for ($i = 0; $i < $n; $i++) {
            $index = $n + 2 * $n - 1 + $n - 1 + $i - $row;
            if ($pos[$i] || $pos[$n + $i + $row] || $pos[$index]) {
                continue;
            }
            $pos[$i] = true;
            $pos[$n + $i + $row] = true;
            $pos[$index] = true;
            $pos2[$row] = $i;
            $this->helper($n, $row + 1, $pos, $pos2, $ans);
            $pos[$i] = false;
            $pos[$n + $i + $row] = false;
            $pos[$index] = false;
        }
    }

    private function construct($n, $pos, &$ans) {
        $sol = array();
        for ($r = 0; $r < $n; $r++) {
            $queenRow = array_fill(0, $n, '.');
            $queenRow[$pos[$r]] = 'Q';
            array_push($sol, implode($queenRow));
        }
        array_push($ans, $sol);
    }
}
```