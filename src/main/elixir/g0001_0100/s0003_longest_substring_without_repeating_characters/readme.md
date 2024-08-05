[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 3\. Longest Substring Without Repeating Characters

Medium

Given a string `s`, find the length of the **longest substring** without repeating characters.

**Example 1:**

**Input:** s = "abcabcbb"

**Output:** 3

**Explanation:** The answer is "abc", with the length of 3. 

**Example 2:**

**Input:** s = "bbbbb"

**Output:** 1

**Explanation:** The answer is "b", with the length of 1. 

**Example 3:**

**Input:** s = "pwwkew"

**Output:** 3

**Explanation:** The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring. 

**Example 4:**

**Input:** s = ""

**Output:** 0 

**Constraints:**

*   <code>0 <= s.length <= 5 * 10<sup>4</sup></code>
*   `s` consists of English letters, digits, symbols and spaces.

## Solution

```elixir
defmodule Solution do
  @spec length_of_longest_substring(s :: String.t()) :: integer
  def length_of_longest_substring(s) do
    sublen([], String.codepoints(s), 0, 0, 0)
  end

  defp sublen(_, [], _, _, m), do: m
  
  defp sublen(left, [next | rest] = right, start, stop, m) do
    if Enum.member?(left, next) do
      [_ | mid] = left
      sublen(mid, right, start + 1, stop, m)
    else
      stop = stop + 1
      sublen(left ++ [next], rest, start, stop, max(m, stop - start))
    end
  end
end
```