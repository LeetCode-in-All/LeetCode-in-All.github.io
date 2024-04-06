[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 300\. Longest Increasing Subsequence

Medium

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, `[3,6,2,7]` is a subsequence of the array `[0,3,1,6,2,2,7]`.

**Example 1:**

**Input:** nums = [10,9,2,5,3,7,101,18]

**Output:** 4

**Explanation:** The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 

**Example 2:**

**Input:** nums = [0,1,0,3,2,3]

**Output:** 4 

**Example 3:**

**Input:** nums = [7,7,7,7,7,7,7]

**Output:** 1 

**Constraints:**

*   `1 <= nums.length <= 2500`
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

**Follow up:** Can you come up with an algorithm that runs in `O(n log(n))` time complexity?

## Solution

```ruby
# @param {Integer[]} nums
# @return {Integer}
def length_of_lis(nums)
  return 0 if nums.nil? || nums.empty?

  dp = Array.new(nums.length + 1, Float::INFINITY)

  left = 1
  right = 1

  nums.each do |curr|
    start_idx = left
    end_idx = right

    # Binary search: find the index where dp[index] is lower than curr
    while start_idx + 1 < end_idx
      mid_idx = start_idx + (end_idx - start_idx) / 2

      if dp[mid_idx] > curr
        end_idx = mid_idx
      else
        start_idx = mid_idx
      end
    end

    # Update the dp table
    if dp[start_idx] > curr
      dp[start_idx] = curr
    elsif curr > dp[start_idx] && curr < dp[end_idx]
      dp[end_idx] = curr
    elsif curr > dp[end_idx]
      dp[end_idx + 1] = curr
      right += 1
    end
  end

  right
end
```