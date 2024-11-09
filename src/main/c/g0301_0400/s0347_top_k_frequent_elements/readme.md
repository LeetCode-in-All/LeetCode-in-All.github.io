[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 347\. Top K Frequent Elements

Medium

Given an integer array `nums` and an integer `k`, return _the_ `k` _most frequent elements_. You may return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,1,1,2,2,3], k = 2

**Output:** [1,2]

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1]

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `k` is in the range `[1, the number of unique elements in the array]`.
*   It is **guaranteed** that the answer is **unique**.

**Follow up:** Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.

## Solution

```c
#include <stdlib.h>
#include <limits.h>

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* topKFrequent(int* nums, int n, int k, int* returnSize) {
    if (n == 0 || k == 0) *returnSize = 0;

    int min_val = INT_MAX;
    int max_val = INT_MIN;
    
    for (int i = 0; i < n; i++) {
        if (nums[i] < min_val) min_val = nums[i];
        if (nums[i] > max_val) max_val = nums[i];
    }

    int range = max_val - min_val + 1;
    int offset = -min_val; 

    // creating frequency array and puttin zero inside as default 

    int* freq = (int*)malloc(range * sizeof(int));
    for (int i = 0; i < range; i++) freq[i] = 0;

    // stroing the frequency in the freq array by ++ opertor 

    for (int i = 0; i < n; i++) freq[nums[i] + offset]++;

    //  finding the k max elemts in the freq array and storing it in result array 
    int* result_1 = (int*)malloc(k * sizeof(int));

    for (int i = 0; i < k; i++) {
        int maxval = -1;
        int max_index = -1;

        for (int j = 0; j < range; j++) {
            if (freq[j] > maxval) {
                maxval = freq[j];
                max_index = j;
            }
        }

        result_1[i] = max_index - offset;
        freq[max_index] = -1;
    }

    *returnSize = k;
    free(freq);
    return result_1;
}
```