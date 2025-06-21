[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 34\. Find First and Last Position of Element in Sorted Array

Medium

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [5,7,7,8,8,10], target = 8

**Output:** [3,4] 

**Example 2:**

**Input:** nums = [5,7,7,8,8,10], target = 6

**Output:** [-1,-1] 

**Example 3:**

**Input:** nums = [], target = 0

**Output:** [-1,-1] 

**Constraints:**

*   <code>0 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
*   `nums` is a non-decreasing array.
*   <code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code>

## Solution

```typescript
function searchRange(nums: number[], target: number): number[] { //NOSONAR
    let first = -1
    let last = -1
    let left1 = 0
    let left2 = left1
    let right1 = nums.length - 1
    let right2 = right1
    while (left1 <= right1 || left2 <= right2) {
        if (left1 <= right1) {
            let mid1 = Math.floor((left1 + right1) / 2)
            if (nums[mid1] == target) {
                first = mid1
                right1 = mid1 - 1
            } else if (nums[mid1] < target) {
                left1 = mid1 + 1
            } else {
                right1 = mid1 - 1
            }
        }
        if (left2 <= right2) {
            let mid2 = Math.floor((left2 + right2) / 2)
            if (nums[mid2] == target) {
                last = mid2
                left2 = mid2 + 1
            } else if (nums[mid2] < target) {
                left2 = mid2 + 1
            } else {
                right2 = mid2 - 1
            }
        }
    }
    return [first, last]
}

export { searchRange }
```