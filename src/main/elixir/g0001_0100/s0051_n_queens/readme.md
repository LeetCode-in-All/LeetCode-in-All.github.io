[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 51\. N-Queens

Hard

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _all distinct solutions to the **n-queens puzzle**_. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

**Input:** n = 4

**Output:** [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]

**Explanation:** There exist two distinct solutions to the 4-queens puzzle as shown above

**Example 2:**

**Input:** n = 1

**Output:** [["Q"]]

**Constraints:**

*   `1 <= n <= 9`

## Solution

```elixir
defmodule Solution do
  @spec solve_n_queens(n :: integer) :: [[String.t]]
  def solve_n_queens(n) do
    solve([], n, {0, 0}, []) |> Enum.map(&normalize(&1, n))
  end
    
  # A board is just a bunch of coordinates where a queen resides.
  defp solve(board, n, {n, 0}, acc), do: [board | acc]
  defp solve(_board, n, {_, n}, acc), do: acc
  defp solve(board, n, {i, j}, acc) do
    acc =
      if attacked?(board, {i, j}) do
        acc
      else
        solve([{i, j} | board], n, {i + 1, 0}, acc)
      end

    solve(board, n, {i, j + 1}, acc)
  end
  
  defp attacked?(board, {i, j}) do
    Enum.any?(board, fn {ii, jj} ->
      jj == j or
        ii - jj == i - j or
        ii + jj == i + j
    end)
  end
    
  defp normalize(board, n) do
    for { {x, y}, i} <- Enum.with_index(board) do
      0..n-1
      |> Enum.map(fn j ->
        if {n - i - 1, j} == {x, y}, do: "Q", else: "."
      end)
      |> IO.iodata_to_binary()
    end
  end
end
```