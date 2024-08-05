[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 22\. Generate Parentheses

Medium

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3

**Output:** ["((()))","(()())","(())()","()(())","()()()"]

**Example 2:**

**Input:** n = 1

**Output:** ["()"]

**Constraints:**

*   `1 <= n <= 8`

## Solution

```elixir
defmodule Solution do
  @spec generate_parenthesis(n :: integer) :: [String.t()]
  def generate_parenthesis(n) do
    generate("", n, n, [])
  end

  defp generate(current, 0, 0, acc) do
    [current | acc]
  end

  defp generate(current, open, close, acc) when open > 0 do
    acc = generate(current <> "(", open - 1, close, acc)
    if open < close do
      generate(current <> ")", open, close - 1, acc)
    else
      acc
    end
  end

  defp generate(current, _open, close, acc) when close > 0 do
    generate(current <> ")", 0, close - 1, acc)
  end
end
```