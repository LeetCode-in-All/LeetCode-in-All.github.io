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

```c
#include <stdlib.h>

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int helper(int* nums, int numsSize, int target, int equals) {
    int l = 0;
    int r = numsSize - 1;
    int result = -1;
    while (l <= r) {
        int mid = l + (r - l) / 2;
        if (nums[mid] == target) {
            result = mid;
        }
        if (nums[mid] < target || (nums[mid] == target && equals)) {
            l = mid + 1;
        } else {
            r = mid - 1;
        }
    }
    return result;
}

int* searchRange(int* nums, int numsSize, int target, int* returnSize) {
    *returnSize = 2;  // There are always two elements in the result
    int* result = (int*)malloc(2 * sizeof(int));
    result[0] = helper(nums, numsSize, target, 0);  // Find the first occurrence
    result[1] = helper(nums, numsSize, target, 1);  // Find the last occurrence
    return result;
}
```