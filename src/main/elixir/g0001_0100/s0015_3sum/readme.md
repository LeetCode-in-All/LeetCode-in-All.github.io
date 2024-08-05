[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 15\. 3Sum

Medium

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

**Input:** nums = [-1,0,1,2,-1,-4]

**Output:** [[-1,-1,2],[-1,0,1]] 

**Example 2:**

**Input:** nums = []

**Output:** [] 

**Example 3:**

**Input:** nums = [0]

**Output:** [] 

**Constraints:**

*   `0 <= nums.length <= 3000`
*   <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>

## Solution

```elixir
defmodule Solution do
  @spec three_sum(nums :: [integer]) :: [[integer]]
  def three_sum(nums) do
    Enum.sort(nums)
    |> Enum.with_index()
    |> find([])
  end

  defp drop_all(list, val) do
    Enum.drop_while(list, fn {x, _} -> x == val end)
  end

  defp find([], ans), do: ans
  defp find([{x, _} | nums], ans) do
    ans =
      Enum.reverse(nums)
      |> two_pointers(nums, x, ans)

    drop_all(nums, x)
    |> find(ans)
  end

  defp two_pointers([], _, _, ans), do: ans
  defp two_pointers(_, [], _, ans), do: ans
  defp two_pointers([{_, j} | _], [{_, i} | _], _, ans)
  when i >= j, do: ans
  
  defp two_pointers([{z, j} | nums2], [{y, i} | nums], x, ans) do
    {nums2, nums, ans} = cond do
      x + y + z == 0 ->
        {drop_all(nums2, z), drop_all(nums, y), [[x, y, z] | ans]}
      x + y + z > 0 -> {drop_all(nums2, z), [{y, i} | nums], ans}
      true -> {[{z, j} | nums2], drop_all(nums, y), ans}
    end

    two_pointers(nums2, nums, x, ans)
  end
end
```