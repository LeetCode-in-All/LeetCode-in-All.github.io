[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 338\. Counting Bits

Easy

Given an integer `n`, return _an array_ `ans` _of length_ `n + 1` _such that for each_ `i` (`0 <= i <= n`)_,_ `ans[i]` _is the **number of**_ `1`_**'s** in the binary representation of_ `i`.

**Example 1:**

**Input:** n = 2

**Output:** [0,1,1]

**Explanation:**

    0 --> 0
    1 --> 1
    2 --> 10 

**Example 2:**

**Input:** n = 5

**Output:** [0,1,1,2,1,2]

**Explanation:**

    0 --> 0
    1 --> 1
    2 --> 10
    3 --> 11
    4 --> 100
    5 --> 101 

**Constraints:**

*   <code>0 <= n <= 10<sup>5</sup></code>

**Follow up:**

*   It is very easy to come up with a solution with a runtime of `O(n log n)`. Can you do it in linear time `O(n)` and possibly in a single pass?
*   Can you do it without using any built-in function (i.e., like `__builtin_popcount` in C++)?

## Solution

```c
#include <stdio.h>
#include <stdlib.h>

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* countBits(int num, int* returnSize) {
    // Allocate memory for the result array and set the return size
    int* result = (int*)malloc((num + 1) * sizeof(int));
    *returnSize = num + 1;

    int borderPos = 1;
    int incrPos = 1;

    result[0] = 0; // Base case: 0 has zero 1-bits

    for (int i = 1; i <= num; i++) {
        // When we reach a power of 2, reset borderPos and incrPos
        if (incrPos == borderPos) {
            result[i] = 1;  // Powers of 2 have exactly one 1-bit
            incrPos = 1;
            borderPos = i;
        } else {
            result[i] = 1 + result[incrPos++];
        }
    }

    return result;
}
```