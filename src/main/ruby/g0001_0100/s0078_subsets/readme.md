[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 78\. Subsets

Medium

Given an integer array `nums` of **unique** elements, return _all possible subsets (the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]] 

**Example 2:**

**Input:** nums = [0]

**Output:** [[],[0]] 

**Constraints:**

*   `1 <= nums.length <= 10`
*   `-10 <= nums[i] <= 10`
*   All the numbers of `nums` are **unique**.

## Solution

```ruby
# @param {Integer[]} nums
# @return {Integer[][]}
def subsets(nums)
  res = []
  subsets = []
  dfs_subsets(0, nums, subsets, res)
  res
end

def dfs_subsets(i, nums, subsets, res)
  return res.append(subsets.clone()) if i >= nums.length
  subsets.append(nums[i])
  dfs_subsets(i + 1, nums, subsets, res)
  subsets.pop()
  dfs_subsets(i + 1, nums, subsets, res)
end
```