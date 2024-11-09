[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 78\. Subsets

Medium

Given an integer array `nums` of **unique** elements, return _all possible subsets (the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

**Example 2:**

**Input:** nums = [0]

**Output:** [[],[0]]

**Constraints:**

*   `1 <= nums.length <= 10`
*   `-10 <= nums[i] <= 10`
*   All the numbers of `nums` are **unique**.

## Solution

```c
#include <stdio.h>
#include <stdlib.h>

/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
void backtrack(int* nums, int numsSize, int** res, int* returnSize, int* returnColumnSizes, int* temp, int tempSize, int start) {
    // Add the current subset to the result
    res[*returnSize] = (int*)malloc((tempSize + 1) * sizeof(int));
    for (int i = 0; i < tempSize; i++) {
        res[*returnSize][i] = temp[i];
    }
    // Mark the end of the subset with -1 (optional)
    res[*returnSize][tempSize] = -1; 
    returnColumnSizes[*returnSize] = tempSize; // Store the size of the current subset
    (*returnSize)++;

    // Generate subsets
    for (int i = start; i < numsSize; i++) {
        temp[tempSize] = nums[i]; // Add current number to the subset
        backtrack(nums, numsSize, res, returnSize, returnColumnSizes, temp, tempSize + 1, i + 1);
    }
}

int** subsets(int* nums, int numsSize, int* returnSize, int** returnColumnSizes) {
    int** res = (int**)malloc(1024 * sizeof(int*)); // Initial allocation for up to 1024 subsets
    *returnSize = 0; // Initialize the count of subsets
    *returnColumnSizes = (int*)malloc(1024 * sizeof(int)); // Initialize sizes array
    int* temp = (int*)malloc(numsSize * sizeof(int)); // Temporary array for current subset

    backtrack(nums, numsSize, res, returnSize, *returnColumnSizes, temp, 0, 0);

    free(temp); // Free temporary array
    return res;
}
```