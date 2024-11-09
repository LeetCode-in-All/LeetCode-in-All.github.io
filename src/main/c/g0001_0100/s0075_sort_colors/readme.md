[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 75\. Sort Colors

Medium

Given an array `nums` with `n` objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

**Example 1:**

**Input:** nums = [2,0,2,1,1,0]

**Output:** [0,0,1,1,2,2]

**Example 2:**

**Input:** nums = [2,0,1]

**Output:** [0,1,2]

**Constraints:**

*   `n == nums.length`
*   `1 <= n <= 300`
*   `nums[i]` is either `0`, `1`, or `2`.

**Follow up:** Could you come up with a one-pass algorithm using only constant extra space?

## Solution

```c
#include <stdio.h>

void sortColors(int* nums, int numsSize) {
    int zeroes = 0; // Count of 0s
    int ones = 0;   // Count of 1s

    // Count the number of 0s and 1s
    for (int i = 0; i < numsSize; i++) {
        if (nums[i] == 0) {
            nums[zeroes++] = 0; // Place 0 at the current zeroes position
        } else if (nums[i] == 1) {
            ones++; // Count the number of 1s
        }
    }

    // Fill in 1s in the next positions
    for (int j = zeroes; j < zeroes + ones; j++) {
        nums[j] = 1;
    }

    // Fill in 2s in the remaining positions
    for (int k = zeroes + ones; k < numsSize; k++) {
        nums[k] = 2;
    }
}
```