[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 79\. Word Search

Medium

Given an `m x n` grid of characters `board` and a string `word`, return `true` _if_ `word` _exists in the grid_.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

**Input:** board = \[\["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"

**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

**Input:** board = \[\["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"

**Output:** true

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

**Input:** board = \[\["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"

**Output:** false

**Constraints:**

*   `m == board.length`
*   `n = board[i].length`
*   `1 <= m, n <= 6`
*   `1 <= word.length <= 15`
*   `board` and `word` consists of only lowercase and uppercase English letters.

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?

## Solution

```elixir
defmodule Solution do
  @spec exist(board :: [[char]], word :: String.t) :: boolean
  def exist(board, word) do
    board =
      board
      |> Enum.map(&List.to_tuple/1)
      |> List.to_tuple()

    w = tuple_size(board) - 1
    h = tuple_size(elem(board, 0)) - 1

    for i <- 0..w, j <- 0..h, reduce: false do
      found -> found || find(board, word, i, j, w, h, [])
    end
  end

  defp find(_board, "", _i, _j, _w, _h, _visited), do: true

  defp find(board, <<char, rest::binary>>, i, j, w, h, visited) do
    cond do
      i < 0 -> false
      i > w -> false
      j < 0 -> false
      j > h -> false
      elem(elem(board, i), j) != char -> false
      {i, j} in visited -> false

      true ->
        visited = [{i, j} | visited]
        find(board, rest, i - 1, j, w, h, visited) ||
        find(board, rest, i + 1, j, w, h, visited) ||
        find(board, rest, i, j - 1, w, h, visited) ||
        find(board, rest, i, j + 1, w, h, visited)
    end
  end
end
```