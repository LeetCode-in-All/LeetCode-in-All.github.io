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

```scala
object Solution {
    def solveNQueens(n: Int): List[List[String]] = {
        val rst = scala.collection.mutable.ListBuffer[List[String]]()
        dfs(n, List[Int](), rst)
        rst.toList
    }

    @SuppressWarnings(Array("scala:S3776"))
    private def dfs(n: Int, oneSol: List[Int], rst: scala.collection.mutable.ListBuffer[List[String]]): Unit = {
        if (oneSol.length == n) {
            val line = for (idx <- oneSol) yield ("." * idx + "Q" + "." * (n - idx - 1))
            rst += line
            return
        }
        for (col <- 0 until n) {
            if (!oneSol.contains(col)) {
                var i = oneSol.length - 1
                var j = col - 1
                var k = col + 1
                var continue = true
                while (continue && i >= 0 && (j >= 0 || k < n)) {
                    if (oneSol(i) == j || oneSol(i) == k) {
                        continue = false
                    }
                    i -= 1
                    j -= 1
                    k += 1
                }
                if (continue) {
                    dfs(n, oneSol :+ col, rst)
                }
            }
        }
    }
}
```