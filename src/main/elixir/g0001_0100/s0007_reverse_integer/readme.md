[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 7\. Reverse Integer

Medium

Given a signed 32-bit integer `x`, return `x` _with its digits reversed_. If reversing `x` causes the value to go outside the signed 32-bit integer range <code>[-2<sup>31</sup>, 2<sup>31</sup> - 1]</code>, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

**Example 1:**

**Input:** x = 123

**Output:** 321 

**Example 2:**

**Input:** x = -123

**Output:** -321 

**Example 3:**

**Input:** x = 120

**Output:** 21 

**Example 4:**

**Input:** x = 0

**Output:** 0 

**Constraints:**

*   <code>-2<sup>31</sup> <= x <= 2<sup>31</sup> - 1</code>

## Solution

```elixir
defmodule Solution do
  @spec reverse(x :: integer) :: integer
  def reverse(x) do
    rev = reverse_digits(x, 0)
    if rev > :math.pow(2, 31) - 1 or rev < -(:math.pow(2, 31)) do
      0
    else
      rev
    end
  end

  defp reverse_digits(0, acc), do: acc

  defp reverse_digits(x, acc) do
    new_acc = (acc * 10) + rem(x, 10)
    reverse_digits(div(x, 10), new_acc)
  end
end
```