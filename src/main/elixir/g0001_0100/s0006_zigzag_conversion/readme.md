[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 6\. Zigzag Conversion

Medium

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P A H N A P L S I I G Y I R 

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

string convert(string s, int numRows); 

**Example 1:**

**Input:** s = "PAYPALISHIRING", numRows = 3

**Output:** "PAHNAPLSIIGYIR" 

**Example 2:**

**Input:** s = "PAYPALISHIRING", numRows = 4

**Output:** "PINALSIGYAHRPI"

**Explanation:** P I N A L S I G Y A H R P I 

**Example 3:**

**Input:** s = "A", numRows = 1

**Output:** "A" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consists of English letters (lower-case and upper-case), `','` and `'.'`.
*   `1 <= numRows <= 1000`

## Solution

```elixir
defmodule Solution do
  @spec convert(s :: String.t, num_rows :: integer) :: String.t
  def convert(s, 1), do: s
  def convert(s, num_rows) do
    String.codepoints(s)
    |> read(%{}, 0, 1, num_rows)
    |> then(fn map ->
      Enum.flat_map(0..num_rows - 1, fn i ->
        Map.get(map, i, [])
        |> Enum.reverse()
      end)
    end)
    |> to_string()
  end

  defp read([], map, _, _, _), do: map
  defp read(s, map, -1, _, num_rows) do
    read(s, map, 1, 1, num_rows)
  end
  defp read(s, map, num_rows, _, num_rows) do
    read(s, map, num_rows - 2, -1, num_rows)
  end
  defp read([ch | s], map, i, add, num_rows) do
    map = Map.update(map, i, [ch], &([ch | &1]))
    read(s, map, i + add, add, num_rows)
  end
end
```