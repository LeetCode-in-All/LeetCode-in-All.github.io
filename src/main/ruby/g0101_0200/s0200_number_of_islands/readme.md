[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 200\. Number of Islands

Medium

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

**Input:**

    grid = [
      ["1","1","1","1","0"],
      ["1","1","0","1","0"],
      ["1","1","0","0","0"],
      ["0","0","0","0","0"]
    ]

**Output:** 1 

**Example 2:**

**Input:**

    grid = [
      ["1","1","0","0","0"],
      ["1","1","0","0","0"],
      ["0","0","1","0","0"],
      ["0","0","0","1","1"]
    ]

**Output:** 3 

**Constraints:**

*   `m == grid.length`
*   `n == grid[i].length`
*   `1 <= m, n <= 300`
*   `grid[i][j]` is `'0'` or `'1'`.

## Solution

```ruby
# @param {Character[][]} grid
# @return {Integer}
def num_islands(grid)
  islands = 0
  if grid && !grid.empty? && !grid[0].empty?
    (0...grid.length).each do |i|
      (0...grid[0].length).each do |j|
        if grid[i][j] == '1'
          dfs_islands(grid, i, j)
          islands += 1
        end
      end
    end
  end
  islands
end

private

def dfs_islands(grid, x, y)
  return if x.negative? || grid.length <= x || y.negative? || grid[0].length <= y || grid[x][y] != '1'

  grid[x][y] = 'x'
  dfs_islands(grid, x + 1, y)
  dfs_islands(grid, x - 1, y)
  dfs_islands(grid, x, y + 1)
  dfs_islands(grid, x, y - 1)
end
```