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

```ruby
# @param {Integer[][]} grid
# @return {Integer}
def min_path_sum(grid)
  return grid[0][0] if grid.length == 1 && grid[0].length == 1

  dm = Array.new(grid.length) {Array.new(grid[0].length, 0)}
  s = 0

  (grid.length - 1).downto(0) do |r|
    dm[r][grid[0].length - 1] = grid[r][grid[0].length - 1] + s
    s += grid[r][grid[0].length - 1]
  end

  s = 0
  (grid[0].length - 1).downto(0) do |c|
    dm[grid.length - 1][c] = grid[grid.length - 1][c] + s
    s += grid[grid.length - 1][c]
  end

  recur(grid, dm, 0, 0)
end

private

def recur(grid, dm, r, c)
  if dm[r][c].zero? && r != grid.length - 1 && c != grid[0].length - 1
    dm[r][c] = grid[r][c] + [recur(grid, dm, r + 1, c), recur(grid, dm, r, c + 1)].min
  end

  dm[r][c]
end
```