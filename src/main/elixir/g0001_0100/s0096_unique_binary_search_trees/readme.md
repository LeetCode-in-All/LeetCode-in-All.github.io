[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 96\. Unique Binary Search Trees

Medium

Given an integer `n`, return _the number of structurally unique **BST'**s (binary search trees) which has exactly_ `n` _nodes of unique values from_ `1` _to_ `n`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

**Input:** n = 3

**Output:** 5

**Example 2:**

**Input:** n = 1

**Output:** 1

**Constraints:**

*   `1 <= n <= 19`

## Solution

```elixir
defmodule Solution do
  @spec num_trees(n :: integer) :: integer
   def num_trees(n) do
    cache = %{0 => 1}
    Enum.reduce(1..n, cache, &unique_trees/2)
    |> Map.get(n)
  end
   def unique_trees(n, cache) do
    count = Enum.map(1..n, fn r ->
      Map.get(cache, r - 1) * Map.get(cache, n - r)
    end)
    |> Enum.sum()
    Map.put(cache, n, count)
  end
end
```