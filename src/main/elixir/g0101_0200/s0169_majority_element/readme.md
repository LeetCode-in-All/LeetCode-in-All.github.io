[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 169\. Majority Element

Easy

Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**

**Input:** nums = [3,2,3]

**Output:** 3

**Example 2:**

**Input:** nums = [2,2,1,1,1,2,2]

**Output:** 2

**Constraints:**

*   `n == nums.length`
*   <code>1 <= n <= 5 * 10<sup>4</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>

**Follow-up:** Could you solve the problem in linear time and in `O(1)` space?

## Solution

```elixir
defmodule Solution do
  @spec majority_element(nums :: [integer]) :: integer
  def majority_element([head | tail]), do: recur(tail, 1, head)

  defp recur([head | tail], 0, _candidate), do: recur(tail, 1, head)

  defp recur([last], _count, candidate) when last === candidate, do: candidate

  defp recur([last, last], _count, candidate) when last === candidate, do: candidate

  defp recur([head | tail], count, candidate) when head === candidate,
    do: recur(tail, count + 1, candidate)

  defp recur([_head | tail], count, candidate), do: recur(tail, count - 1, candidate)

  defp recur([], _count, candidate), do: candidate
end
```