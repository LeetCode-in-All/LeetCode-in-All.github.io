[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 53\. Maximum Subarray

Medium

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return _its sum_.

A **subarray** is a **contiguous** part of an array.

**Example 1:**

**Input:** nums = [-2,1,-3,4,-1,2,1,-5,4]

**Output:** 6

**Explanation:** [4,-1,2,1] has the largest sum = 6.

**Example 2:**

**Input:** nums = [1]

**Output:** 1

**Example 3:**

**Input:** nums = [5,4,-1,7,8]

**Output:** 23

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

**Follow up:** If you have figured out the `O(n)` solution, try coding another solution using the **divide and conquer** approach, which is more subtle.

## Solution

```elixir
defmodule Solution do
  @spec max_sub_array(nums :: [integer]) :: integer
  def max_sub_array([h | t]) do
    solve(t, h, h)
  end

  defp solve([], curr_sum, max_sum), do: max(curr_sum, max_sum)

  defp solve(nums, curr_sum, max_sum) when curr_sum < 0 do
    solve(nums, 0, max_sum)
  end

  defp solve([h | t], curr_sum, max_sum) do
    curr_sum = curr_sum + h
    solve(t, curr_sum, max(curr_sum, max_sum))
  end
end
```