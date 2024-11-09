[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 31\. Next Permutation

Medium

A **permutation** of an array of integers is an arrangement of its members into a sequence or linear order.

*   For example, for `arr = [1,2,3]`, the following are all the permutations of `arr`: `[1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1]`.

The **next permutation** of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the **next permutation** of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

*   For example, the next permutation of `arr = [1,2,3]` is `[1,3,2]`.
*   Similarly, the next permutation of `arr = [2,3,1]` is `[3,1,2]`.
*   While the next permutation of `arr = [3,2,1]` is `[1,2,3]` because `[3,2,1]` does not have a lexicographical larger rearrangement.

Given an array of integers `nums`, _find the next permutation of_ `nums`.

The replacement must be **[in place](http://en.wikipedia.org/wiki/In-place_algorithm)** and use only constant extra memory.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [1,3,2]

**Example 2:**

**Input:** nums = [3,2,1]

**Output:** [1,2,3]

**Example 3:**

**Input:** nums = [1,1,5]

**Output:** [1,5,1]

**Constraints:**

*   `1 <= nums.length <= 100`
*   `0 <= nums[i] <= 100`

## Solution

```c
#include <stdio.h>

// Function to swap two elements in the array
void swap(int* nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}

// Function to reverse elements in the array from index i to j
void reverse(int* nums, int i, int j) {
    while (i < j) {
        swap(nums, i++, j--);
    }
}

// Function to find the next permutation
void nextPermutation(int* nums, int numsSize) {
    if (nums == NULL || numsSize <= 1) {
        return;
    }

    int i = numsSize - 2;
    // Find the first decreasing element from the end
    while (i >= 0 && nums[i] >= nums[i + 1]) {
        i--;
    }

    if (i >= 0) {
        int j = numsSize - 1;
        // Find the element just larger than nums[i]
        while (nums[j] <= nums[i]) {
            j--;
        }
        swap(nums, i, j);
    }

    // Reverse the elements after the found index to get the next smallest lexicographic order
    reverse(nums, i + 1, numsSize - 1);
}
```