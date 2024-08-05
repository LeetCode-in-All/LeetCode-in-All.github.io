[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 32\. Longest Valid Parentheses

Hard

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

**Example 1:**

**Input:** s = "(()"

**Output:** 2

**Explanation:** The longest valid parentheses substring is "()".

**Example 2:**

**Input:** s = ")()())"

**Output:** 4

**Explanation:** The longest valid parentheses substring is "()()".

**Example 3:**

**Input:** s = ""

**Output:** 0

**Constraints:**

*   <code>0 <= s.length <= 3 * 10<sup>4</sup></code>
*   `s[i]` is `'('`, or `')'`.

## Solution

```elixir
defmodule Solution do
  @spec longest_valid_parentheses(s :: String.t()) :: integer
  def longest_valid_parentheses(s) do
    s
    |> String.graphemes()
    |> dp([], 0)
  end

  def dp([], _, result), do: result

  def dp(["(" | tail], queue, result) do
    dp(tail, [0 | queue], result)
  end

  def dp([")" | tail], queue, result) do
    {new_queue, new_result} = pop_until(queue, [])

    dp(tail, new_queue, max(result, new_result))
  end

  def pop_until([], _), do: {[], 0}

  def pop_until([0 | tail], rest) do
    n = List.first(tail)
    n = if n, do: n, else: 0
    tail = if n > 0, do: tl(tail), else: tail
    result = Enum.sum(rest) + n + 2
    
    {[result | tail], result}
  end


  def pop_until([h | tail], rest) do
    pop_until(tail, [h | rest])
  end
end
```