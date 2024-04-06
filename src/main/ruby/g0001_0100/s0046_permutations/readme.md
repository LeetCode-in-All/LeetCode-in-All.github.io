[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 46\. Permutations

Medium

Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]] 

**Example 2:**

**Input:** nums = [0,1]

**Output:** [[0,1],[1,0]] 

**Example 3:**

**Input:** nums = [1]

**Output:** [[1]] 

**Constraints:**

*   `1 <= nums.length <= 6`
*   `-10 <= nums[i] <= 10`
*   All the integers of `nums` are **unique**.

## Solution

```ruby
# @param {Integer[]} nums
# @return {Integer[][]}
def permute(nums)
  return [] if nums.nil? || nums.empty?

  final_result = []
  permute_recur(nums, final_result, [], Array.new(nums.length, false))
  final_result
end

private

def permute_recur(nums, final_result, curr_result, used)
  if curr_result.length == nums.length
    final_result << curr_result.dup
    return
  end

  nums.each_with_index do |num, i|
    next if used[i]

    curr_result << num
    used[i] = true
    permute_recur(nums, final_result, curr_result, used)
    used[i] = false
    curr_result.pop
  end
end
```