[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 5\. Longest Palindromic Substring

Medium

Given a string `s`, return _the longest palindromic substring_ in `s`.

**Example 1:**

**Input:** s = "babad"

**Output:** "bab" **Note:** "aba" is also a valid answer. 

**Example 2:**

**Input:** s = "cbbd"

**Output:** "bb" 

**Example 3:**

**Input:** s = "a"

**Output:** "a" 

**Example 4:**

**Input:** s = "ac"

**Output:** "a" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consist of only digits and English letters.

## Solution

```elixir
defmodule Solution do
  @spec longest_palindrome(s :: String.t()) :: String.t()
  def longest_palindrome(<<>>), do: ""
  def longest_palindrome(<<f::binary-size(1)>>), do: f
  def longest_palindrome(s) do
    {ri,rj} =String.to_charlist(s) |> List.to_tuple |>  do_longest_palindrome(0, {0,0})
    String.slice(s,ri..rj)
  end

  defp do_longest_palindrome(s_t,i,{ri,rj}) when i == tuple_size(s_t), do: {ri,rj}
  defp do_longest_palindrome(s_t,i,{ri,rj}) do
    {ri,rj} = do_longest_palindrome(s_t,i,i,{ri,rj})
    {ri,rj} = do_longest_palindrome(s_t,i,i+1,{ri,rj})
    do_longest_palindrome(s_t, i+1, {ri, rj})
  end

  defp do_longest_palindrome(s_t,i,j,{ri,rj}) when (i<0 or j==tuple_size(s_t)) or (elem(s_t,i) != elem(s_t,j)) do
    if ((j-1)-(i+1)) > rj-ri, do: {i+1,j-1}, else: {ri,rj}
  end
  defp do_longest_palindrome(s_t,i,j,{ri,rj}), do: do_longest_palindrome(s_t, i-1, j+1, {ri,rj})
end
```