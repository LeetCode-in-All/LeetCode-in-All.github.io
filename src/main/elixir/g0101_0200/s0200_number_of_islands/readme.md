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

```elixir
defmodule Solution do
  @spec num_islands(grid :: [[char]]) :: integer
  def num_islands(grid) do
    lands = grid |> Enum.with_index() |> Enum.reduce(MapSet.new(), fn {line, i}, lands ->
      line |> Enum.with_index() |> Enum.reduce(lands, fn {is_land?, j}, lands ->
        if is_land? == ?0 do
          lands
        else
          MapSet.put(lands, {i, j})
        end
      end)
    end)

    lands |> Enum.reduce({MapSet.new(), 0}, fn land, {visited, count}->
      if MapSet.member?(visited, land) do
        {visited, count}
      else
        visited = visit_island(visited, lands, land)
        {visited, count + 1}
      end
    end) |> elem(1)
  end

  defp visit_island(visited, lands, {i, j} = land) do
    with true <- MapSet.member?(lands, land),
         false <- MapSet.member?(visited, land) do
      visited
      |> MapSet.put(land)
      |> visit_island(lands, {i - 1, j})
      |> visit_island(lands, {i + 1, j})
      |> visit_island(lands, {i, j - 1})
      |> visit_island(lands, {i, j + 1})
    else
      _ -> visited
    end
  end
end
```