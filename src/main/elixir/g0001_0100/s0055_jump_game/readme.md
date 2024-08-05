[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 55\. Jump Game

Medium

You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` _if you can reach the last index, or_ `false` _otherwise_.

**Example 1:**

**Input:** nums = [2,3,1,1,4]

**Output:** true

**Explanation:** Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

**Input:** nums = [3,2,1,0,4]

**Output:** false

**Explanation:** You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   <code>0 <= nums[i] <= 10<sup>5</sup></code>

## Solution

```elixir
defmodule Solution do
  @spec can_jump(nums :: [integer]) :: boolean
  def can_jump(nums) do
    can?(0, length(nums) - 1, nums)
  end

  defp can?(reach, dist, _) when reach >= dist, do: true
  defp can?(reach, _, _) when reach < 0, do: false
  defp can?(reach, dist, [head | tail]) do
    can?(max(reach, head) - 1, dist - 1, tail)
  end
end
```