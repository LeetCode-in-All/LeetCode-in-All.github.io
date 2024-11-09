[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 33\. Search in Rotated Sorted Array

Medium

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return _the index of_ `target` _if it is in_ `nums`_, or_ `-1` _if it is not in_ `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [4,5,6,7,0,1,2], target = 0

**Output:** 4

**Example 2:**

**Input:** nums = [4,5,6,7,0,1,2], target = 3

**Output:** -1

**Example 3:**

**Input:** nums = [1], target = 0

**Output:** -1

**Constraints:**

*   `1 <= nums.length <= 5000`
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   All values of `nums` are **unique**.
*   `nums` is an ascending array that is possibly rotated.
*   <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>

## Solution

```c
#include <stdio.h>

int search(int* nums, int numsSize, int target) {
    int lo = 0;
    int hi = numsSize - 1;
    int mid;

    while (lo <= hi) {
        mid = ((hi - lo) >> 1) + lo;

        if (nums[mid] == target) {
            return mid;
        }

        // Check if the left half is sorted
        if (nums[lo] <= nums[mid]) {
            // Target is in the left half
            if (nums[lo] <= target && target <= nums[mid]) {
                hi = mid - 1;
            } else { // Target is in the right half
                lo = mid + 1;
            }
        }
        // Otherwise, the right half is sorted
        else {
            // Target is in the right half
            if (nums[mid] <= target && target <= nums[hi]) {
                lo = mid + 1;
            } else { // Target is in the left half
                hi = mid - 1;
            }
        }
    }

    return -1;
}
```