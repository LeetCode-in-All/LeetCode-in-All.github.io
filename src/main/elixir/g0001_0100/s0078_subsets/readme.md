[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 78\. Subsets

Medium

Given an integer array `nums` of **unique** elements, return _all possible subsets (the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

**Example 2:**

**Input:** nums = [0]

**Output:** [[],[0]]

**Constraints:**

*   `1 <= nums.length <= 10`
*   `-10 <= nums[i] <= 10`
*   All the numbers of `nums` are **unique**.

## Solution

```elixir
defmodule Solution do
   @spec subsets(nums :: [integer]) :: [[integer]]
  def subsets(nums) do
    arr_lenth = length(nums)

    0..arr_lenth
    |> Enum.reduce([], fn x, acc ->
      Enum.concat(combinations(x, nums), acc)
    end)
    |> Enum.sort_by(&length/1)
  end

  def combinations(0, _), do: [[]]
  def combinations(_, []), do: []

  def combinations(size, [head | tail]) do
    for elem <- combinations(size - 1, tail) do
      [head | elem]
    end ++ combinations(size, tail)
  end
end
```