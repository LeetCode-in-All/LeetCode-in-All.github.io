[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 152\. Maximum Product Subarray

Medium

Given an integer array `nums`, find a contiguous non-empty subarray within the array that has the largest product, and return _the product_.

The test cases are generated so that the answer will fit in a **32-bit** integer.

A **subarray** is a contiguous subsequence of the array.

**Example 1:**

**Input:** nums = [2,3,-2,4]

**Output:** 6

**Explanation:** [2,3] has the largest product 6.

**Example 2:**

**Input:** nums = [-2,0,-1]

**Output:** 0

**Explanation:** The result cannot be 2, because [-2,-1] is not a subarray.

**Constraints:**

*   <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
*   `-10 <= nums[i] <= 10`
*   The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

## Solution

```c
#include <stdio.h>
#include <limits.h>

// Function to get the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Function to get the minimum of two integers
int min(int a, int b) {
    return (a < b) ? a : b;
}

// Function to find the maximum product subarray
int maxProduct(int* nums, int numsSize) {
    if (numsSize == 0) return 0;

    int currentMaxProd = nums[0];
    int currentMinProd = nums[0];
    int overAllMaxProd = nums[0];

    for (int i = 1; i < numsSize; i++) {
        if (nums[i] < 0) {
            // Swap currentMaxProd and currentMinProd
            int temp = currentMaxProd;
            currentMaxProd = currentMinProd;
            currentMinProd = temp;
        }

        // Update the current maximum and minimum products
        currentMaxProd = max(nums[i], nums[i] * currentMaxProd);
        currentMinProd = min(nums[i], nums[i] * currentMinProd);

        // Update the overall maximum product
        overAllMaxProd = max(overAllMaxProd, currentMaxProd);
    }

    return overAllMaxProd;
}
```