[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 494\. Target Sum

Medium

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

*   For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

**Example 1:**

**Input:** nums = [1,1,1,1,1], target = 3

**Output:** 5

**Explanation:**

    There are 5 ways to assign symbols to make the sum of nums be target 3.
    -1 + 1 + 1 + 1 + 1 = 3
    +1 - 1 + 1 + 1 + 1 = 3
    +1 + 1 - 1 + 1 + 1 = 3
    +1 + 1 + 1 - 1 + 1 = 3
    +1 + 1 + 1 + 1 - 1 = 3 

**Example 2:**

**Input:** nums = [1], target = 1

**Output:** 1 

**Constraints:**

*   `1 <= nums.length <= 20`
*   `0 <= nums[i] <= 1000`
*   `0 <= sum(nums[i]) <= 1000`
*   `-1000 <= target <= 1000`

## Solution

```ruby
# @param {Integer[]} nums
# @param {Integer} target
# @return {Integer}
def find_target_sum_ways(nums, s)
  sum = nums.sum
  s = s.abs

  # Invalid s, just return 0
  return 0 if s > sum || (sum + s).odd?

  dp = Array.new((sum + s) / 2 + 1) {Array.new(nums.length + 1, 0)}
  dp[0][0] = 1

  # empty knapsack must be processed specially
  nums.each_with_index do |num, i|
    dp[0][i + 1] = num.zero? ? dp[0][i] * 2 : dp[0][i]
  end

  (1...dp.length).each do |i|
    (0...nums.length).each do |j|
      dp[i][j + 1] += dp[i][j]
      dp[i][j + 1] += dp[i - nums[j]][j] if nums[j] <= i
    end
  end

  dp[(sum + s) / 2][nums.length]
end
```