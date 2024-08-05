[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 74\. Search a 2D Matrix

Medium

Write an efficient algorithm that searches for a value `target` in an `m x n` integer matrix `matrix`. This matrix has the following properties:

*   Integers in each row are sorted from left to right.
*   The first integer of each row is greater than the last integer of the previous row.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

**Input:** matrix = \[\[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3

**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

**Input:** matrix = \[\[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13

**Output:** false

**Constraints:**

*   `m == matrix.length`
*   `n == matrix[i].length`
*   `1 <= m, n <= 100`
*   <code>-10<sup>4</sup> <= matrix[i][j], target <= 10<sup>4</sup></code>

## Solution

```elixir
defmodule Solution do
  @spec search_matrix(matrix :: [[integer]], target :: integer) :: boolean
  def search_matrix(matrix, target) do
    matrix = matrix |> Enum.map(&List.to_tuple/1) |> List.to_tuple()
    binary_search(matrix, 0, tuple_size(matrix) * tuple_size(elem(matrix, 0)) - 1, target)
  end

  defp binary_search(_matrix, left, right, _target) when left > right, do: false

  defp binary_search(matrix, left, right, target) do
    mid = div(right + left, 2)
    cols = matrix |> elem(0) |> tuple_size()
    mid_elem = matrix |> elem(div(mid, cols)) |> elem(rem(mid, cols))

    cond do
      mid_elem > target -> binary_search(matrix, left, right - 1, target)
      mid_elem < target -> binary_search(matrix, mid + 1, right, target)
      mid_elem == target -> true
    end
  end
end
```