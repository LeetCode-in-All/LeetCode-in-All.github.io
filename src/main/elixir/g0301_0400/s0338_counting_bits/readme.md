[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 338\. Counting Bits

Easy

Given an integer `n`, return _an array_ `ans` _of length_ `n + 1` _such that for each_ `i` (`0 <= i <= n`)_,_ `ans[i]` _is the **number of**_ `1`_**'s** in the binary representation of_ `i`.

**Example 1:**

**Input:** n = 2

**Output:** [0,1,1]

**Explanation:**

    0 --> 0
    1 --> 1
    2 --> 10 

**Example 2:**

**Input:** n = 5

**Output:** [0,1,1,2,1,2]

**Explanation:**

    0 --> 0
    1 --> 1
    2 --> 10
    3 --> 11
    4 --> 100
    5 --> 101 

**Constraints:**

*   <code>0 <= n <= 10<sup>5</sup></code>

**Follow up:**

*   It is very easy to come up with a solution with a runtime of `O(n log n)`. Can you do it in linear time `O(n)` and possibly in a single pass?
*   Can you do it without using any built-in function (i.e., like `__builtin_popcount` in C++)?

## Solution

```elixir
defmodule Solution do
  @spec count_bits(n :: integer) :: [integer]
  def count_bits(n), do: do_count_bits(1, n, Map.new(0..div(n,2), &({&1,0})), [0])

  defp do_count_bits(i, n, map, acc) when i > n, do: Enum.reverse(acc)
  defp do_count_bits(i, n, map, acc) do
    i_bits = map[div(i,2)] + rem(i,2)
    new_map = if i > div(n,2), do: map, else: Map.put(map, i, i_bits)
    do_count_bits(i + 1, n, new_map, [i_bits | acc])
  end
end
```