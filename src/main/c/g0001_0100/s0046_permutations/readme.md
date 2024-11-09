[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 46\. Permutations

Medium

Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

**Example 2:**

**Input:** nums = [0,1]

**Output:** [[0,1],[1,0]]

**Example 3:**

**Input:** nums = [1]

**Output:** [[1]]

**Constraints:**

*   `1 <= nums.length <= 6`
*   `-10 <= nums[i] <= 10`
*   All the integers of `nums` are **unique**.

## Solution

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
void addResult(int** result, int* returnSize, int* columnSizes, int* currResult, int numsSize) {
    result[*returnSize] = malloc(numsSize * sizeof(int));
    for (int i = 0; i < numsSize; i++) {
        result[*returnSize][i] = currResult[i];
    }
    columnSizes[*returnSize] = numsSize;
    (*returnSize)++;
}

void permuteRecur(int* nums, int numsSize, int** result, int* returnSize, int* columnSizes, int* currResult, bool* used, int currIndex) {
    if (currIndex == numsSize) {
        addResult(result, returnSize, columnSizes, currResult, numsSize);
        return;
    }
    for (int i = 0; i < numsSize; i++) {
        if (used[i]) {
            continue;
        }
        currResult[currIndex] = nums[i];
        used[i] = true;
        permuteRecur(nums, numsSize, result, returnSize, columnSizes, currResult, used, currIndex + 1);
        used[i] = false;
    }
}

int** permute(int* nums, int numsSize, int* returnSize, int** returnColumnSizes) {
    int** result = malloc(1000 * sizeof(int*));  // Allocate space for result
    *returnSize = 0;
    *returnColumnSizes = malloc(1000 * sizeof(int)); // Allocate space for column sizes

    bool* used = calloc(numsSize, sizeof(bool));
    int* currResult = malloc(numsSize * sizeof(int));

    permuteRecur(nums, numsSize, result, returnSize, *returnColumnSizes, currResult, used, 0);

    free(used);
    free(currResult);

    return result;
}
```