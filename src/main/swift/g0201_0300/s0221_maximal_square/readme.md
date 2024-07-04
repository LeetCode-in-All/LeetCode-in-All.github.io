[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 221\. Maximal Square

Medium

Given an `m x n` binary `matrix` filled with `0`'s and `1`'s, _find the largest square containing only_ `1`'s _and return its area_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/max1grid.jpg)

**Input:** matrix = \[\["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]

**Output:** 4 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/26/max2grid.jpg)

**Input:** matrix = \[\["0","1"],["1","0"]]

**Output:** 1 

**Example 3:**

**Input:** matrix = \[\["0"]]

**Output:** 0 

**Constraints:**

*   `m == matrix.length`
*   `n == matrix[i].length`
*   `1 <= m, n <= 300`
*   `matrix[i][j]` is `'0'` or `'1'`.

## Solution

```swift
class Solution {
    func maximalSquare(_ matrix: [[Character]]) -> Int {
        guard matrix.count > 0 && matrix[0].count > 0 else { return 0 }
        var square = Array(repeating: Array(repeating: 0, count: matrix[0].count), count: matrix.count)
        var curMaxLen = 0
        
        for i in 0..<matrix.count {
            for j in 0..<matrix[0].count {
                // when first col or row, set value manually, avoid "-1" index as well
                if i == 0 || j == 0 {
                    square[i][j] = Int(String(matrix[i][j]))!
                }
                else if matrix[i][j] == "1" {
                    square[i][j] = min(min(square[i-1][j], square[i][j-1]), square[i-1][j-1]) + 1
                }
                curMaxLen = max(curMaxLen, square[i][j])
            }
        }
        return curMaxLen*curMaxLen
    }
}
```