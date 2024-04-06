[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 287\. Find the Duplicate Number

Medium

Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return _this repeated number_.

You must solve the problem **without** modifying the array `nums` and uses only constant extra space.

**Example 1:**

**Input:** nums = [1,3,4,2,2]

**Output:** 2 

**Example 2:**

**Input:** nums = [3,1,3,4,2]

**Output:** 3 

**Example 3:**

**Input:** nums = [1,1]

**Output:** 1 

**Example 4:**

**Input:** nums = [1,1,2]

**Output:** 1 

**Constraints:**

*   <code>1 <= n <= 10<sup>5</sup></code>
*   `nums.length == n + 1`
*   `1 <= nums[i] <= n`
*   All the integers in `nums` appear only **once** except for **precisely one integer** which appears **two or more** times.

**Follow up:**

*   How can we prove that at least one duplicate number must exist in `nums`?
*   Can you solve the problem in linear runtime complexity?

## Solution

```ruby
# @param {Integer[]} nums
# @return {Integer}
def find_duplicate(nums)
  arr = Array.new(nums.length + 1, 0)

  nums.each do |num|
    arr[num] += 1
    return num if arr[num] == 2
  end

  0
end
```