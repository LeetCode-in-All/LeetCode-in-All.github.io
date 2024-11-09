[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 763\. Partition Labels

Medium

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return _a list of integers representing the size of these parts_.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"

**Output:** [9,7,8]

**Explanation:** The partition is "ababcbaca", "defegde", "hijhklij". This is a partition so that each letter appears in at most one part. A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.

**Example 2:**

**Input:** s = "eccbbbbdec"

**Output:** [10]

**Constraints:**

*   `1 <= s.length <= 500`
*   `s` consists of lowercase English letters.

## Solution

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* partitionLabels(char* s, int* returnSize) {
    int position[26] = {0}; // Last occurrence positions for each letter
    int length = strlen(s);

    // Populate the position array with the last index of each character
    for (int i = 0; i < length; i++) {
        position[s[i] - 'a'] = i;
    }

    // Initialize an array to store partition sizes
    int* result = (int*)malloc(length * sizeof(int));
    *returnSize = 0; // Set returnSize to 0 initially
    int prev = -1;
    int max = 0;

    // Iterate through the string to find partitions
    for (int i = 0; i < length; i++) {
        if (position[s[i] - 'a'] > max) {
            max = position[s[i] - 'a'];
        }
        if (i == max) {
            result[*returnSize] = i - prev;
            (*returnSize)++;
            prev = i;
        }
    }

    // Resize the result array to the exact number of partitions found
    result = (int*)realloc(result, (*returnSize) * sizeof(int));
    return result;
}
```