[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 215\. Kth Largest Element in an Array

Medium

Given an integer array `nums` and an integer `k`, return _the_ <code>k<sup>th</sup></code> _largest element in the array_.

Note that it is the <code>k<sup>th</sup></code> largest element in the sorted order, not the <code>k<sup>th</sup></code> distinct element.

You must solve it in `O(n)` time complexity.

**Example 1:**

**Input:** nums = [3,2,1,5,6,4], k = 2

**Output:** 5

**Example 2:**

**Input:** nums = [3,2,3,1,2,4,5,5,6], k = 4

**Output:** 4

**Constraints:**

*   <code>1 <= k <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

## Solution

```c
#include <stdbool.h>
#include <stdlib.h>

int findKthLargest(int* nums, int numsSize, int k) {
    int positiveArr[10001] = {0};
    int negativeArr[10001] = {0};
    int cumulativeCount = 0;
    int result = 0;
    bool found = false;

    // Count occurrences of each element
    for (int i = 0; i < numsSize; i++) {
        if (nums[i] >= 0) {
            positiveArr[nums[i]]++;
        } else {
            negativeArr[abs(nums[i])]++;
        }
    }

    // Search for the k-th largest in positive numbers
    for (int i = 10000; i >= 0; i--) {
        cumulativeCount += positiveArr[i];
        if (cumulativeCount >= k) {
            result = i;
            found = true;
            break;
        }
    }

    // If k-th largest is not found in positive numbers, search in negative numbers
    if (!found) {
        for (int i = 1; i <= 10000; i++) {
            cumulativeCount += negativeArr[i];
            if (cumulativeCount >= k) {
                result = -i;
                break;
            }
        }
    }

    return result;
}
```