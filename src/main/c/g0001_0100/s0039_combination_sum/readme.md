[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 39\. Combination Sum

Medium

Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is **guaranteed** that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

**Example 1:**

**Input:** candidates = [2,3,6,7], target = 7

**Output:** [[2,2,3],[7]]

**Explanation:** 
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.

7 is a candidate, and 7 = 7. 

These are the only two combinations.

**Example 2:**

**Input:** candidates = [2,3,5], target = 8

**Output:** [[2,2,2,2],[2,3,3],[3,5]]

**Example 3:**

**Input:** candidates = [2], target = 1

**Output:** []

**Constraints:**

*   `1 <= candidates.length <= 30`
*   `1 <= candidates[i] <= 200`
*   All elements of `candidates` are **distinct**.
*   `1 <= target <= 500`

## Solution

```c
#include <stdlib.h>
#include <string.h>

/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */

int compareInt(void *a, void *b) {
    return (*(int *)a) - (*(int *)b);
}

void combinationRec(int *arr, int n, int pos, int target, int **seq, int pos1, int **res, int *resP, int **cols) {
    int *seq2;

    if (target == 0) {
        res[*resP] = *seq;
        (*cols)[*resP] = pos1;
        *resP += 1;
        return;
    }

    if (pos == n || arr[pos] > target) {
        free(*seq);
        return;
    }

    seq2 = malloc(40 * sizeof(int));
    memcpy(seq2, *seq, 40 * sizeof(int));

    (*seq)[pos1++] = arr[pos];
    combinationRec(arr, n, pos, target - arr[pos], seq, pos1, res, resP, cols);

    combinationRec(arr, n, pos + 1, target, &seq2, pos1 - 1, res, resP, cols);
}

int **combinationSum(int *candidates, int candidatesSize, int target, int *returnSize, int **returnColumnSizes) {
    int *seq = malloc(40 * sizeof(int));
    int **res = malloc(200 * sizeof(int *));
    int resP = 0;
    int *cols = malloc(200 * sizeof(int));

    qsort(candidates, candidatesSize, sizeof(int), compareInt);
    combinationRec(candidates, candidatesSize, 0, target, &seq, 0, res, &resP, &cols);

    *returnSize = resP;
    *returnColumnSizes = cols;

    return res;
}
```