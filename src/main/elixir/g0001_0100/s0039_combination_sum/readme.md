[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 39\. Combination Sum

Medium

Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is **guaranteed** that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

**Example 1:**

**Input:** candidates = [2,3,6,7], target = 7

**Output:** [[2,2,3],[7]]

**Explanation:** 
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.

7 is a candidate, and 7 = 7. 

These are the only two combinations.

**Example 2:**

**Input:** candidates = [2,3,5], target = 8

**Output:** [[2,2,2,2],[2,3,3],[3,5]]

**Example 3:**

**Input:** candidates = [2], target = 1

**Output:** []

**Constraints:**

*   `1 <= candidates.length <= 30`
*   `1 <= candidates[i] <= 200`
*   All elements of `candidates` are **distinct**.
*   `1 <= target <= 500`

## Solution

```elixir
defmodule Solution do
  @spec combination_sum(candidates :: [integer], target :: integer) :: [[integer]]
  def combination_sum(candidates, target) do
    combination_sum_rec(candidates, target, [], [])
  end

  defp combination_sum_rec(_, 0, sublist, ans) do
    [Enum.reverse(sublist) | ans]
  end

  defp combination_sum_rec([], _, _, ans) do
    ans
  end

  defp combination_sum_rec([h | t], target, sublist, ans) when target >= h do
    ans_with_h = combination_sum_rec([h | t], target - h, [h | sublist], ans)
    combination_sum_rec(t, target, sublist, ans_with_h)
  end

  defp combination_sum_rec([_ | t], target, sublist, ans) do
    combination_sum_rec(t, target, sublist, ans)
  end
end
```