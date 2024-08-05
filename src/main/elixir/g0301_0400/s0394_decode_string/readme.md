[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 394\. Decode String

Medium

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed <code>10<sup>5</sup></code>.

**Example 1:**

**Input:** s = "3[a]2[bc]"

**Output:** "aaabcbc"

**Example 2:**

**Input:** s = "3[a2[c]]"

**Output:** "accaccacc"

**Example 3:**

**Input:** s = "2[abc]3[cd]ef"

**Output:** "abcabccdcdcdef"

**Constraints:**

*   `1 <= s.length <= 30`
*   `s` consists of lowercase English letters, digits, and square brackets `'[]'`.
*   `s` is guaranteed to be **a valid** input.
*   All the integers in `s` are in the range `[1, 300]`.

## Solution

```elixir
defmodule Solution do
  @spec decode_string(s :: String.t()) :: String.t()
  def decode_string(s) do
    decode_string_helper(s, 0, [])
    |> elem(0)
    |> Enum.reverse()
    |> List.to_string()
  end

  defp decode_string_helper(s, i, acc) do
    if i >= String.length(s) do
      {acc, i}
    else
      case String.at(s, i) do
        <<c>> when c in ?a..?z or c in ?A..?Z ->
          decode_string_helper(s, i + 1, [c | acc])

        <<c>> when c in ?0..?9 ->
          {count, i} = parse_number(s, i)
          {repeat, i} = decode_string_helper(s, i + 1, [])
          repeated = Enum.flat_map(1..count, fn _ -> repeat end)
          decode_string_helper(s, i, repeated ++ acc)

        "]" ->
          {acc, i + 1}

        _ ->
          decode_string_helper(s, i + 1, acc)
      end
    end
  end

  defp parse_number(s, i) do
    parse_number(s, i, 0)
  end

  defp parse_number(s, i, acc) do
    if i < String.length(s) and String.at(s, i) =~ ~r/\d/ do
      acc = acc * 10 + String.to_integer(String.at(s, i))
      parse_number(s, i + 1, acc)
    else
      {acc, i}
    end
  end
end
```