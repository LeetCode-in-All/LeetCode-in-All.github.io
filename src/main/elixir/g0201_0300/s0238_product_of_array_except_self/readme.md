[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 238\. Product of Array Except Self

Medium

Given an integer array `nums`, return _an array_ `answer` _such that_ `answer[i]` _is equal to the product of all the elements of_ `nums` _except_ `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

**Input:** nums = [1,2,3,4]

**Output:** [24,12,8,6]

**Example 2:**

**Input:** nums = [-1,1,0,-3,3]

**Output:** [0,0,9,0,0]

**Constraints:**

*   <code>2 <= nums.length <= 10<sup>5</sup></code>
*   `-30 <= nums[i] <= 30`
*   The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

**Follow up:** Can you solve the problem in `O(1) `extra space complexity? (The output array **does not** count as extra space for space complexity analysis.)

## Solution

```elixir
defmodule Solution do
  @spec product_except_self(nums :: [integer]) :: [integer]
  def product_except_self(nums) do
    elem(pes(nums, 1), 0)
  end

  def pes([], _), do: {[], 1}
  
  # cur_prod is an accumulator to keep track of product 
  # of all elements we've seen 
  @spec pes(nums :: [integer], cur_prod :: integer) :: {[integer], integer}
  def pes([num | nums], cur_prod) do
    {pes_list, next_prod} = pes(nums, cur_prod * num)

    # cur_prod * next_prod is the product of all elements in list
    # except the current element `num`. We also return num * next_prod
    # so previous recursive calls of this fn can have the product of all
    # elements in the list after them.
    {[cur_prod * next_prod | pes_list], num * next_prod}
  end
end
```