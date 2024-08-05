[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 416\. Partition Equal Subset Sum

Medium

Given a **non-empty** array `nums` containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Example 1:**

**Input:** nums = [1,5,11,5]

**Output:** true

**Explanation:** The array can be partitioned as [1, 5, 5] and [11].

**Example 2:**

**Input:** nums = [1,2,3,5]

**Output:** false

**Explanation:** The array cannot be partitioned into equal sum subsets.

**Constraints:**

*   `1 <= nums.length <= 200`
*   `1 <= nums[i] <= 100`

## Solution

```elixir
defmodule Solution do
  @spec can_partition(nums :: [integer]) :: boolean
  def can_partition(nums) do
    sum = Enum.sum(nums)

    if rem(sum, 2) != 0 do
      false
    else
      target = div(sum, 2)

      for n <- nums, s <- target..n, reduce: %{0 => true} do
        dp -> Map.put(dp, s, Map.get(dp, s, false) || Map.get(dp, s - n, false))
      end
      |> Map.get(target)
    end
  end
end
```