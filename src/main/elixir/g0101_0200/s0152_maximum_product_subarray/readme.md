[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 152\. Maximum Product Subarray

Medium

Given an integer array `nums`, find a contiguous non-empty subarray within the array that has the largest product, and return _the product_.

The test cases are generated so that the answer will fit in a **32-bit** integer.

A **subarray** is a contiguous subsequence of the array.

**Example 1:**

**Input:** nums = [2,3,-2,4]

**Output:** 6

**Explanation:** [2,3] has the largest product 6.

**Example 2:**

**Input:** nums = [-2,0,-1]

**Output:** 0

**Explanation:** The result cannot be 2, because [-2,-1] is not a subarray.

**Constraints:**

*   <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
*   `-10 <= nums[i] <= 10`
*   The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

## Solution

```elixir
defmodule Solution do
  @spec max_product(nums :: [integer]) :: integer
  def max_product(nums) do
    nums
    |> Stream.chunk_by(& &1 == 0)
    |> Stream.map(&max_prod/1)
    |> Enum.max()
  end
      
  defp max_prod([0 | _]), do: 0
                            
  defp max_prod([n]), do: n
                            
  defp max_prod(chunk) do
    prod = Enum.product(chunk)
    max(
      div_till_pos(prod, chunk),
      div_till_pos(prod, Enum.reverse(chunk))
    )
  end
      
  defp div_till_pos(prod, _) when prod > 0, do: prod
  defp div_till_pos(prod, [n | t]), do: prod |> div(n) |> div_till_pos(t)
end
```