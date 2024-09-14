[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 200\. Number of Islands

Medium

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

**Input:** grid = [ 

["1","1","1","1","0"], 

["1","1","0","1","0"], 

["1","1","0","0","0"], 

["0","0","0","0","0"] 

]

**Output:** 1

**Example 2:**

**Input:** grid = [ 

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

```rust
impl Solution {
    pub fn num_islands(grid: Vec<Vec<char>>) -> i32 {
        let mut num_of_islands: i32 = 0;
        let mut current_index: i32 = 1;
        let height = grid.len();
        let width = grid[0].len();
        let mut part_of_island = vec![0; width * height];
        let mut pos;

        for current in 0..height * width {
            let x = current / width;
            let y = current % width;

            if grid[x][y] == '1' {
                let left = if y > 0 {
                    part_of_island[current - 1]
                } else {
                    0
                };

                let up = if x > 0 {
                    part_of_island[current - width]
                } else {
                    0
                };

                if up > 1 {
                    if left > 1 && left != up {
                        for i in 0..width {
                            pos = part_of_island[current - i];
                            if pos == left {
                                part_of_island[current - i] = up;
                            }
                        }
                        num_of_islands -= 1;
                    }
                    part_of_island[current] = up;
                    continue;
                } else if left > 1 {
                    part_of_island[current] = left;
                    continue;
                }

                current_index += 1;
                num_of_islands += 1;
                part_of_island[current] = current_index;
            }
        }

        num_of_islands
    }
}
```