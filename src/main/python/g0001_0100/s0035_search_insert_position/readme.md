[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 35\. Search Insert Position

Easy

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [1,3,5,6], target = 5

**Output:** 2 

**Example 2:**

**Input:** nums = [1,3,5,6], target = 2

**Output:** 1 

**Example 3:**

**Input:** nums = [1,3,5,6], target = 7

**Output:** 4 

**Example 4:**

**Input:** nums = [1,3,5,6], target = 0

**Output:** 0 

**Example 5:**

**Input:** nums = [1], target = 0

**Output:** 0 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `nums` contains **distinct** values sorted in **ascending** order.
*   <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>

To solve this problem efficiently with a runtime complexity of O(log n), we can use binary search to find the insertion position of the target value in the sorted array. 

## Solution

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        low = 0
        high = len(nums) - 1

        while low <= high:
            mid = int((low + high) / 2)
            guess = nums[mid]

            if(guess == target):
                return mid

            elif guess < target:
                low = mid + 1
                if nums[-1] == guess:
                    return mid + 1
                elif nums[low] > target:
                    return mid + 1              
            else: 
                high = mid - 1
                 
        return mid
```