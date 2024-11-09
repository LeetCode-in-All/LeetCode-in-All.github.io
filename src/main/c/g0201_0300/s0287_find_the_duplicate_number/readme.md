[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 287\. Find the Duplicate Number

Medium

Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return _this repeated number_.

You must solve the problem **without** modifying the array `nums` and uses only constant extra space.

**Example 1:**

**Input:** nums = [1,3,4,2,2]

**Output:** 2

**Example 2:**

**Input:** nums = [3,1,3,4,2]

**Output:** 3

**Constraints:**

*   <code>1 <= n <= 10<sup>5</sup></code>
*   `nums.length == n + 1`
*   `1 <= nums[i] <= n`
*   All the integers in `nums` appear only **once** except for **precisely one integer** which appears **two or more** times.

**Follow up:**

*   How can we prove that at least one duplicate number must exist in `nums`?
*   Can you solve the problem in linear runtime complexity?

## Solution

```c
#include <stdio.h>

int findDuplicate(int* nums, int numsSize) {
    // Create an array of size numsSize + 1, initialized to 0
    int arr[numsSize + 1];
    for (int i = 0; i <= numsSize; i++) {
        arr[i] = 0;
    }

    // Iterate over the nums array and update the arr counts
    for (int i = 0; i < numsSize; i++) {
        arr[nums[i]] += 1;
        if (arr[nums[i]] == 2) {
            return nums[i];  // Return the duplicate element
        }
    }

    return 0;  // In case no duplicate is found, though the problem assumes there is always a duplicate
}
```