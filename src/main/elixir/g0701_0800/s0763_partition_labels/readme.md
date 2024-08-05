[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 763\. Partition Labels

Medium

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return _a list of integers representing the size of these parts_.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"

**Output:** [9,7,8]

**Explanation:** The partition is "ababcbaca", "defegde", "hijhklij". This is a partition so that each letter appears in at most one part. A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.

**Example 2:**

**Input:** s = "eccbbbbdec"

**Output:** [10]

**Constraints:**

*   `1 <= s.length <= 500`
*   `s` consists of lowercase English letters.

## Solution

```elixir
defmodule Solution do
  @spec partition_labels(s :: String.t()) :: [integer]
  def partition_labels(s) do
    letters = String.graphemes(s)
    position = Enum.reduce(0..(length(letters) - 1), %{}, fn i, acc ->
      Map.put(acc, Enum.at(letters, i), i)
    end)

    partition_labels(letters, position, 0, -1, 0, [])
  end

  defp partition_labels([], _position, _i, prev, _max, result) do
    Enum.reverse(result)
  end

  defp partition_labels([letter | rest], position, i, prev, max, result) do
    current_max = Map.get(position, letter)

    # Update the maximum index to which the current partition must extend
    new_max = max(current_max, max)

    # If we have reached the end of the current partition
    if i == new_max do
      # Add the size of the partition to the result list
      new_result = [i - prev | result]
      partition_labels(rest, position, i + 1, i, 0, new_result)
    else
      partition_labels(rest, position, i + 1, prev, new_max, result)
    end
  end
end
```