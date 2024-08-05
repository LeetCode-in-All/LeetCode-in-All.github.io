[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 62\. Unique Paths

Medium

There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return _the number of possible unique paths that the robot can take to reach the bottom-right corner_.

The test cases are generated so that the answer will be less than or equal to <code>2 * 10<sup>9</sup></code>.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

**Input:** m = 3, n = 7

**Output:** 28

**Example 2:**

**Input:** m = 3, n = 2

**Output:** 3

**Explanation:** From the top-left corner, there are a total of 3 ways to reach the bottom-right corner: 

1. Right -> Down -> Down 

2. Down -> Down -> Right 

3. Down -> Right -> Down

**Constraints:**

*   `1 <= m, n <= 100`

## Solution

```elixir
defmodule Solution do
  @spec unique_paths(m :: integer, n :: integer) :: integer
  def unique_paths(m, n) do
    ncr(m + n - 2, min(m, n) - 1)
  end

  defp ncr(n, r) do
    Enum.reduce(1..r#1, 1, fn i, acc ->
      div(acc * (i + n - r), i)
    end)
  end
end
```