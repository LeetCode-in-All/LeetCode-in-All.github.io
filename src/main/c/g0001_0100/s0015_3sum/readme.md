[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 15\. 3Sum

Medium

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

**Input:** nums = [-1,0,1,2,-1,-4]

**Output:** [[-1,-1,2],[-1,0,1]] 

**Example 2:**

**Input:** nums = []

**Output:** [] 

**Example 3:**

**Input:** nums = [0]

**Output:** [] 

**Constraints:**

*   `0 <= nums.length <= 3000`
*   <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>

## Solution

```c
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int compare(const void* a, const void* b) {
    return (*(int*)a - *(int*)b);
}

int** threeSum(int* nums, int numsSize, int* returnSize, int** returnColumnSizes) {
    qsort(nums, numsSize, sizeof(int), compare);

    int **ret_arr = (int**)malloc(sizeof(int*) * numsSize * numsSize);
    *returnColumnSizes = (int*)malloc(sizeof(int) * numsSize * numsSize);
    int row = 0;
    int col = 3;

    for (int i = 0; i < numsSize - 2; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) {
            continue;
        }

        int j = i + 1;
        int k = numsSize - 1;

        while (j < k) {
            int sum = nums[i] + nums[j] + nums[k];
            if (sum == 0) {
                ret_arr[row] = (int*)malloc(sizeof(int) * col);
                (*returnColumnSizes)[row] = col;
                ret_arr[row][0] = nums[i];
                ret_arr[row][1] = nums[j];
                ret_arr[row][2] = nums[k];
                row++;

                while (j < k && nums[j + 1] == nums[j]) j++;
                while (j < k && nums[k - 1] == nums[k]) k--;

                j++;
                k--;
            } else if (sum < 0) {
                j++;
            } else {
                k--;
            }
        }
    }

    *returnSize = row;
    return ret_arr;
}
```