[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 128\. Longest Consecutive Sequence

Medium

Given an unsorted array of integers `nums`, return _the length of the longest consecutive elements sequence._

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

**Input:** nums = [100,4,200,1,3,2]

**Output:** 4

**Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4.

**Example 2:**

**Input:** nums = [0,3,7,2,5,8,4,6,0,1]

**Output:** 9

**Constraints:**

*   <code>0 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>

## Solution

```elixir
defmodule Solution do
  @spec longest_consecutive(nums :: [integer]) :: integer
  def longest_consecutive(nums) do
    nums 
      |> Enum.sort()
      |> count_consecutive([1])
      |> Enum.max() # find max 
  end

  defp count_consecutive(nums = [head_1, head_2 | tail], 
                         seq_lens = [seq_head | _seq_tail]) do
    new_len = 
      case (head_1 - head_2) do
        -1 -> seq_head + 1 # element is consecutive, increment
        0  -> seq_head     # element is same, do nothing
        _  -> 1            # element not consecutive, reset count
      end

    # Prepend count of consecutive elements
    count_consecutive([head_2 | tail], [new_len | seq_lens]) 
  end

  defp count_consecutive([_h | []], seq_lens), do: seq_lens # terminates when list is empty

  defp count_consecutive([], [_h | []]), do: [0] # runs if list has single number
end
```