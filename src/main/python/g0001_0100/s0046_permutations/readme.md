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

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        if not nums:
            return []
        
        final_result = []
        self.permute_recur(nums, final_result, [], [False] * len(nums))
        return final_result

    def permute_recur(self, nums: List[int], final_result: List[List[int]], curr_result: List[int], used: List[bool]):
        if len(curr_result) == len(nums):
            final_result.append(curr_result.copy())
            return
        
        for i in range(len(nums)):
            if used[i]:
                continue
            curr_result.append(nums[i])
            used[i] = True
            self.permute_recur(nums, final_result, curr_result, used)
            used[i] = False
            curr_result.pop()
```