[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 17\. Letter Combinations of a Phone Number

Medium

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**Example 1:**

**Input:** digits = "23"

**Output:** ["ad","ae","af","bd","be","bf","cd","ce","cf"]

**Example 2:**

**Input:** digits = ""

**Output:** []

**Example 3:**

**Input:** digits = "2"

**Output:** ["a","b","c"]

**Constraints:**

*   `0 <= digits.length <= 4`
*   `digits[i]` is a digit in the range `['2', '9']`.

## Solution

```elixir
defmodule Solution do
  @t9 (Enum.chunk_every(?a..?o, 3) ++ [~c"pqrs", ~c"tuv", ~c"wxyz"])
      |> Enum.with_index(2)
      |> Map.new(fn {a, n} -> {n, a} end)

  @spec letter_combinations(digits :: String.t()) :: [String.t()]
  def letter_combinations(""), do: []

  def letter_combinations(digits) do
    digits
    |> String.to_integer()
    |> Integer.digits()
    |> Enum.map(&Map.get(@t9, &1))
    |> Enum.reduce([~c""], fn l, acc ->
      for x <- acc,
          y <- l do
        x ++ [y]
      end
    end)
    |> Enum.map(&to_string/1)
  end
end
```