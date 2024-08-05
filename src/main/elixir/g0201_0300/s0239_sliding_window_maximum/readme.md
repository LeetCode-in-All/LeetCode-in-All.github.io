[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 239\. Sliding Window Maximum

Hard

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

**Example 1:**

**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3

**Output:** [3,3,5,5,6,7]

**Explanation:** 

Window position Max 

--------------- ----- 

[1 3 -1] -3 5 3 6 7 **3** 

1 [3 -1 -3] 5 3 6 7 **3** 

1 3 [-1 -3 5] 3 6 7 **5** 

1 3 -1 [-3 5 3] 6 7 **5** 

1 3 -1 -3 [5 3 6] 7 **6** 

1 3 -1 -3 5 [3 6 7] **7**

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1]

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `1 <= k <= nums.length`

## Solution

```elixir
defmodule Solution do
  @spec max_sliding_window(nums :: [integer], k :: integer) :: [integer]
  def max_sliding_window(nums, k) do
    Enum.with_index(nums)
    |> Enum.map_reduce(:queue.new(), fn {x, i}, q ->
      enqueue(q, x, i)
      |> get_max(i - k)
    end)
    |> elem(0)
    |> Enum.drop(k - 1)
  end

  defp enqueue(q, x, i) do
    case :queue.peek_r(q) do
      {:value, {y, _}} when y <= x ->
        :queue.drop_r(q)
        |> enqueue(x, i)
      _ -> :queue.in({x, i}, q)
    end
  end

  defp get_max(q, drop_until) do
    case :queue.peek(q) do
      {:value, {_, j}} when j <= drop_until ->
        :queue.drop(q)
        |> get_max(drop_until)
      {:value, {y, _}} -> {y, q}
    end
  end
end
```