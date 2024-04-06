[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 41\. First Missing Positive

Hard

Given an unsorted integer array `nums`, return the smallest missing positive integer.

You must implement an algorithm that runs in `O(n)` time and uses constant extra space.

**Example 1:**

**Input:** nums = [1,2,0]

**Output:** 3 

**Example 2:**

**Input:** nums = [3,4,-1,1]

**Output:** 2 

**Example 3:**

**Input:** nums = [7,8,9,11,12]

**Output:** 1 

**Constraints:**

*   <code>1 <= nums.length <= 5 * 10<sup>5</sup></code>
*   <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>

## Solution

```ruby
# @param {Integer[]} nums
# @return {Integer}
def first_missing_positive(nums)
  nums.each_with_index do |num, i|
    next if num <= 0 || num > nums.length || num == i + 1

    dfs(nums, num)
  end

  nums.each_with_index do |num, i|
    return i + 1 if num != i + 1
  end

  nums.length + 1
end

private

def dfs(nums, val)
  return if val <= 0 || val > nums.length || val == nums[val - 1]

  temp = nums[val - 1]
  nums[val - 1] = val
  dfs(nums, temp)
end
```