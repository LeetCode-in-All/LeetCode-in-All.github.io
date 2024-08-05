[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 647\. Palindromic Substrings

Medium

Given a string `s`, return _the number of **palindromic substrings** in it_.

A string is a **palindrome** when it reads the same backward as forward.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "abc"

**Output:** 3

**Explanation:** Three palindromic strings: "a", "b", "c".

**Example 2:**

**Input:** s = "aaa"

**Output:** 6

**Explanation:** Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consists of lowercase English letters.

## Solution

```elixir
defmodule Solution do
  @spec count_substrings(s :: String.t()) :: integer
  def count_substrings(s) do
    tuple_s =
      s
      |> String.graphemes()
      |> List.to_tuple()

    get_count(tuple_s, 0, 0)
  end

  def get_count(tuple_s, count, i) when i >= tuple_size(tuple_s) do
    count
  end

  def get_count(tuple_s, count, i) do
    left = right = i
    count = count + while(tuple_s, 0, left, right)

    left = i
    right = i + 1
    count = count + while(tuple_s, 0, left, right)

    get_count(tuple_s, count, i + 1)
  end

  def while(tuple_s, acc, left, right)
      when left < 0 or
             right >= tuple_size(tuple_s) or
             elem(tuple_s, left) != elem(tuple_s, right) do
    acc
  end

  def while(tuple_s, acc, left, right) do
    while(tuple_s, acc + 1, left - 1, right + 1)
  end
end
```