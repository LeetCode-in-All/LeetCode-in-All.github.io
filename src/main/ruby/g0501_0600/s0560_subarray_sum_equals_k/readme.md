[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 560\. Subarray Sum Equals K

Medium

Given an array of integers `nums` and an integer `k`, return _the total number of continuous subarrays whose sum equals to `k`_.

**Example 1:**

**Input:** nums = [1,1,1], k = 2

**Output:** 2 

**Example 2:**

**Input:** nums = [1,2,3], k = 3

**Output:** 2 

**Constraints:**

*   <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
*   `-1000 <= nums[i] <= 1000`
*   <code>-10<sup>7</sup> <= k <= 10<sup>7</sup></code>

## Solution

```ruby
# @param {Integer[]} nums
# @param {Integer} k
# @return {Integer}
def subarray_sum(nums, k)
  temp_sum = 0
  ret = 0
  sum_count = {0 => 1}

  nums.each do |i|
    temp_sum += i
    ret += sum_count[temp_sum - k] if sum_count[temp_sum - k]
    sum_count[temp_sum] = sum_count[temp_sum].to_i + 1
  end

  ret
end
```