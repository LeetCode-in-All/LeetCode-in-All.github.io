[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 41\. First Missing Positive

Hard

Given an unsorted integer array `nums`, return the smallest missing positive integer.

You must implement an algorithm that runs in `O(n)` time and uses constant extra space.

**Example 1:**

**Input:** nums = [1,2,0]

**Output:** 3

**Explanation:** The numbers in the range [1,2] are all in the array.

**Example 2:**

**Input:** nums = [3,4,-1,1]

**Output:** 2

**Explanation:** 1 is in the array but 2 is missing.

**Example 3:**

**Input:** nums = [7,8,9,11,12]

**Output:** 1

**Explanation:** The smallest positive integer 1 is missing.

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>

## Solution

```elixir
defmodule Solution do
  @spec first_missing_positive(nums :: [integer]) :: integer
  def first_missing_positive(nums) do
    nums
    |> Enum.sort()
    |> find_missing_num()
  end

  defp find_missing_num(nums, acc \\ 1)

  defp find_missing_num([], acc) do
    acc
  end

  defp find_missing_num([h | t], acc) do
    acc = if h == acc, do: acc + 1, else: acc
    find_missing_num(t, acc)
  end
end
```