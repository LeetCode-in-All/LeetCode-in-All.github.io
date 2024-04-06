[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 64\. Minimum Path Sum

Medium

Given a `m x n` `grid` filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

**Input:** grid = \[\[1,3,1],[1,5,1],[4,2,1]]

**Output:** 7

**Explanation:** Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum. 

**Example 2:**

**Input:** grid = \[\[1,2,3],[4,5,6]]

**Output:** 12 

**Constraints:**

*   `m == grid.length`
*   `n == grid[i].length`
*   `1 <= m, n <= 200`
*   `0 <= grid[i][j] <= 100`

## Solution

```php
class Solution {
    /**
     * @param Integer[][] $grid
     * @return Integer
     */
    public function minPathSum($a) {
        for ($i = 1; $i < count($a); $i++) {
            $a[$i][0] += $a[$i - 1][0];
        }
        for ($j = 1; $j < count($a[0]); $j++) {
            $a[0][$j] += $a[0][$j - 1];
        }
        for ($i = 1; $i < count($a); $i++) {
            for ($j = 1; $j < count($a[0]); $j++) {
                $a[$i][$j] += min($a[$i - 1][$j], $a[$i][$j - 1]);
            }
        }
        return $a[count($a) - 1][count($a[0]) - 1];
    }
}
```