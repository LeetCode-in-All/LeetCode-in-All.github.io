[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 56\. Merge Intervals

Medium

Given an array of `intervals` where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code>, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

**Input:** intervals = \[\[1,3],[2,6],[8,10],[15,18]]

**Output:** [[1,6],[8,10],[15,18]]

**Explanation:** Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

**Example 2:**

**Input:** intervals = \[\[1,4],[4,5]]

**Output:** [[1,5]]

**Explanation:** Intervals [1,4] and [4,5] are considered overlapping.

**Constraints:**

*   <code>1 <= intervals.length <= 10<sup>4</sup></code>
*   `intervals[i].length == 2`
*   <code>0 <= start<sub>i</sub> <= end<sub>i</sub> <= 10<sup>4</sup></code>

## Solution

```c
#include <stdio.h>
#include <stdlib.h>

/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int compare(const void* a, const void* b) {
    return (*(int**)a)[0] - (*(int**)b)[0];
}

int** merge(int** intervals, int intervalsSize, int* intervalsColSize, int* returnSize, int** returnColumnSizes) {
    // Step 1: Sort the intervals based on the starting times
    qsort(intervals, intervalsSize, sizeof(int*), compare);

    // Step 2: Create a dynamic array to hold merged intervals
    int** merged = (int**)malloc(intervalsSize * sizeof(int*));
    *returnColumnSizes = (int*)malloc(intervalsSize * sizeof(int));
    *returnSize = 0;

    // Initialize the current interval as the first one
    int* current = intervals[0];
    merged[(*returnSize)++] = (int*)malloc(2 * sizeof(int));
    merged[0][0] = current[0];
    merged[0][1] = current[1];

    // Step 3: Iterate through the intervals
    for (int i = 1; i < intervalsSize; i++) {
        int* next = intervals[i];
        // Check if there is an overlap
        if (current[1] >= next[0]) {
            current[1] = (current[1] > next[1]) ? current[1] : next[1]; // Merge
            merged[*returnSize - 1][1] = current[1]; // Update the last merged interval
        } else {
            current = next; // Move to the next interval
            merged[(*returnSize)++] = (int*)malloc(2 * sizeof(int));
            merged[*returnSize - 1][0] = current[0];
            merged[*returnSize - 1][1] = current[1];
        }
    }

    // Step 4: Allocate return column sizes
    for (int i = 0; i < *returnSize; i++) {
        (*returnColumnSizes)[i] = 2; // Each merged interval has size 2
    }

    return merged;
}
```