[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 131\. Palindrome Partitioning

Medium

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

**Example 1:**

**Input:** s = "aab"

**Output:** [["a","a","b"],["aa","b"]]

**Example 2:**

**Input:** s = "a"

**Output:** [["a"]]

**Constraints:**

*   `1 <= s.length <= 16`
*   `s` contains only lowercase English letters.

## Solution

```elixir
defmodule Solution do
  use Agent

  @spec partition(s :: String.t()) :: [[String.t()]]
  def partition(s) do
    dfs(s, String.length(s), 0, [], [])
  end

  def dfs(_s, len, l, subs, ans) when l == len do
    [Enum.reverse(subs) | ans]
  end

  def dfs(s, len, l, subs, ans) do
    l..(len - 1)
    |> Enum.reduce(ans, fn r, ans ->
      ss = String.slice(s, l..r)

      if ss == String.reverse(ss) do
        dfs(s, len, r + 1, [ss | subs], ans)
      else
        ans
      end
    end)
  end
end
```