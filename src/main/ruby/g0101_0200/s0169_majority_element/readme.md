[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 169\. Majority Element

Easy

Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**

**Input:** nums = [3,2,3]

**Output:** 3 

**Example 2:**

**Input:** nums = [2,2,1,1,1,2,2]

**Output:** 2 

**Constraints:**

*   `n == nums.length`
*   <code>1 <= n <= 5 * 10<sup>4</sup></code>
*   <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>

**Follow-up:** Could you solve the problem in linear time and in `O(1)` space?

## Solution

```ruby
# @param {Integer[]} nums
# @return {Integer}
def majority_element(nums)
  candidate_count = 0
  candidate_letter = nil

  nums.each_with_object({}) do |num, hash|
    hash[num] = 1 + hash[num] ||= 0
  end.each do |k, v|
    next if candidate_count >= v

    candidate_letter = k
    candidate_count = v
  end

  candidate_letter
end
```