[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 34\. Find First and Last Position of Element in Sorted Array

Medium

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [5,7,7,8,8,10], target = 8

**Output:** [3,4]

**Example 2:**

**Input:** nums = [5,7,7,8,8,10], target = 6

**Output:** [-1,-1]

**Example 3:**

**Input:** nums = [], target = 0

**Output:** [-1,-1]

**Constraints:**

*   <code>0 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
*   `nums` is a non-decreasing array.
*   <code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code>

## Solution

```elixir
defmodule Solution do
  @spec search_range(nums :: [integer], target :: integer) :: [integer]
  def search_range([], _), do: [-1, -1]
  def search_range(nums, target) do
    tuple = list_to_tuple(nums)
    left = find_left(tuple, 0, tuple_size(tuple) - 1, target)
    right = find_right(tuple, 0, tuple_size(tuple) - 1, target)
    [left, right]
  end

  defp find_left(nums, left, left, target), do: if elem(nums, left) == target, do: left, else: -1
  defp find_left(nums, left, right, target) do
    mid = left + div((right - left), 2)
    if (target <= elem(nums, mid)) do
      cond do
        elem(nums, left) == target -> left
        elem(nums, left) < target -> find_left(nums, left, mid, target)
        true -> -1
      end
    else
      find_left(nums, mid + 1, right, target)
    end
  end

  defp find_right(nums, right, right, target), do: if elem(nums, right) == target, do: right, else: -1
  defp find_right(nums, left, right, target) do
    mid = left + div((right - left + 1), 2) 
    if (target >= elem(nums, mid)) do
      cond do
        elem(nums, right) == target -> right
        elem(nums, right) > target -> find_right(nums, mid, right, target)
        true -> -1
      end
    else
      find_right(nums, left, mid - 1, target)
    end
  end

  defp list_to_tuple(list), do: list_to_tuple(list, {})
  defp list_to_tuple([], tuple), do: tuple
  defp list_to_tuple([x|xs], tuple), do: list_to_tuple(xs, Tuple.append(tuple, x))
end
```