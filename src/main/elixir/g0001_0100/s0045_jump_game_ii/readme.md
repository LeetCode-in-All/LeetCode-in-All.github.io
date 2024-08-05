[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 45\. Jump Game II

Medium

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

**Example 1:**

**Input:** nums = [2,3,1,1,4]

**Output:** 2

**Explanation:** The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

**Input:** nums = [2,3,0,1,4]

**Output:** 2

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   `0 <= nums[i] <= 1000`

## Solution

```elixir
defmodule Solution do
  @spec jump(nums :: [integer]) :: integer
  def jump(nums) do
    min_jump(nums, 0, 0, length(nums) - 1, 0)
  end
  
  defp min_jump(_, move, _, dest, ans) when move >= dest, do: ans
  defp min_jump(_, _, next_move, dest, ans) when next_move >= dest, do: ans + 1
  defp min_jump([x | nums], 0, next_move, dest, ans) do
    min_jump(nums, max(x, next_move) - 1, 0, dest - 1, ans + 1)
  end
  defp min_jump([x | nums], move, next_move, dest, ans) do
    min_jump(nums, move - 1, max(x, next_move) - 1, dest - 1, ans)
  end
end
```