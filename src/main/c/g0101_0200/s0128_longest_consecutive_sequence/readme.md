[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 128\. Longest Consecutive Sequence

Medium

Given an unsorted array of integers `nums`, return _the length of the longest consecutive elements sequence._

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

**Input:** nums = [100,4,200,1,3,2]

**Output:** 4

**Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4.

**Example 2:**

**Input:** nums = [0,3,7,2,5,8,4,6,0,1]

**Output:** 9

**Constraints:**

*   <code>0 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>

## Solution

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

int compare(const void* a, const void* b) {
    return (*(int*)a - *(int*)b);
}

int longestConsecutive(int* nums, int numsSize) {
    if (numsSize == 0) {
        return 0;
    }

    // Sort the array
    qsort(nums, numsSize, sizeof(int), compare);

    int max = INT_MIN;
    int thsMax = 1;

    for (int i = 0; i < numsSize - 1; i++) {
        if (nums[i + 1] == nums[i] + 1) {
            thsMax += 1;
        } else if (nums[i + 1] != nums[i]) {
            // Update max if current sequence is longer
            if (thsMax > max) {
                max = thsMax;
            }
            thsMax = 1; // Reset thsMax for a new sequence
        }
    }
    
    // Check the last sequence length
    if (thsMax > max) {
        max = thsMax;
    }

    return max;
}
```