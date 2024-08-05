[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 72\. Edit Distance

Hard

Given two strings `word1` and `word2`, return _the minimum number of operations required to convert `word1` to `word2`_.

You have the following three operations permitted on a word:

*   Insert a character
*   Delete a character
*   Replace a character

**Example 1:**

**Input:** word1 = "horse", word2 = "ros"

**Output:** 3

**Explanation:** 

horse -> rorse (replace 'h' with 'r') 

rorse -> rose (remove 'r') 

rose -> ros (remove 'e')

**Example 2:**

**Input:** word1 = "intention", word2 = "execution"

**Output:** 5

**Explanation:** 

intention -> inention (remove 't') 

inention -> enention (replace 'i' with 'e') 

enention -> exention (replace 'n' with 'x') 

exention -> exection (replace 'n' with 'c') 

exection -> execution (insert 'u')

**Constraints:**

*   `0 <= word1.length, word2.length <= 500`
*   `word1` and `word2` consist of lowercase English letters.

## Solution

```elixir
defmodule Solution do
  @spec min_distance(word1 :: String.t, word2 :: String.t) :: integer
  def min_distance(word1, word2) do
    for {ch1, i} <- [" " | String.codepoints(word1)] |> Enum.with_index(),
    {ch2, j} <- [" " | String.codepoints(word2)] |> Enum.with_index(),
    reduce: %{} do map ->
      cond do
        i == 0 -> j
        j == 0 -> i
        ch1 == ch2 -> Map.get(map, {i - 1, j - 1})
        true ->
          Map.get(map, {i - 1, j})
          |> min(Map.get(map, {i - 1, j - 1}))
          |> min(Map.get(map, {i, j - 1}))
          |> Kernel.+(1)
      end
      |> then(&(Map.put(map, {i, j}, &1)))
    end
    |> Map.get({String.length(word1), String.length(word2)})
  end
end
```