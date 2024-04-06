[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 53\. Maximum Subarray

Easy

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return _its sum_.

A **subarray** is a **contiguous** part of an array.

**Example 1:**

**Input:** nums = [-2,1,-3,4,-1,2,1,-5,4]

**Output:** 6

**Explanation:** [4,-1,2,1] has the largest sum = 6. 

**Example 2:**

**Input:** nums = [1]

**Output:** 1 

**Example 3:**

**Input:** nums = [5,4,-1,7,8]

**Output:** 23 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

**Follow up:** If you have figured out the `O(n)` solution, try coding another solution using the **divide and conquer** approach, which is more subtle.

## Solution

```ruby
# @param {Integer[]} nums
# @return {Integer}
def max_sub_array(nums)
  sum_so_far = 0
  max_sum = -Float::INFINITY
  end_ptr = 0

  while end_ptr < nums.length
    sum_so_far += nums[end_ptr]
    max_sum = [max_sum, sum_so_far].max
    sum_so_far = 0 if sum_so_far < 0

    end_ptr += 1
  end

  max_sum
end
```