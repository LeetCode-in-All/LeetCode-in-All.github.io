[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 15\. 3Sum

Medium

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

**Input:** nums = [-1,0,1,2,-1,-4]

**Output:** [[-1,-1,2],[-1,0,1]] 

**Example 2:**

**Input:** nums = []

**Output:** [] 

**Example 3:**

**Input:** nums = [0]

**Output:** [] 

**Constraints:**

*   `0 <= nums.length <= 3000`
*   <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>

## Solution

```ruby
# @param {Integer[]} nums
# @return {Integer[][]}
def three_sum(nums)
  nums = nums.sort
  rs = []
  nums.each.with_index do |num, i|
    if i > 0 && num == nums[i - 1]
      next
    end
    l, r = i + 1, nums.size - 1

    while l < r
      sum = num + nums[l] + nums[r]
      if sum > 0
        r -= 1
      elsif sum < 0
        l += 1
      else
        rs << [num, nums[l], nums[r]]
        l += 1
        while nums[l] == nums[l - 1] && l < r
          l += 1
        end
      end
    end
  end

  rs
end
```