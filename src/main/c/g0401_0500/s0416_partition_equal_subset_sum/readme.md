[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 416\. Partition Equal Subset Sum

Medium

Given a **non-empty** array `nums` containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Example 1:**

**Input:** nums = [1,5,11,5]

**Output:** true

**Explanation:** The array can be partitioned as [1, 5, 5] and [11].

**Example 2:**

**Input:** nums = [1,2,3,5]

**Output:** false

**Explanation:** The array cannot be partitioned into equal sum subsets.

**Constraints:**

*   `1 <= nums.length <= 200`
*   `1 <= nums[i] <= 100`

## Solution

```c
#include <stdio.h>
#include <stdbool.h>

bool canPartition(int* nums, int numsSize) {
    int sums = 0;
    
    // Calculate the total sum of the array
    for (int i = 0; i < numsSize; i++) {
        sums += nums[i];
    }

    // If the total sum is odd, it's not possible to partition
    if (sums % 2 != 0) {
        return false;
    }

    // The target sum is half of the total sum
    sums /= 2;

    // Create a dynamic programming array to check for possible sums
    bool dp[sums + 1];
    
    // Initialize the dp array to false
    for (int i = 0; i <= sums; i++) {
        dp[i] = false;
    }
    
    dp[0] = true;  // Base case: sum of 0 is always possible

    // Iterate over each number in the array
    for (int i = 0; i < numsSize; i++) {
        // Update the dp array in reverse to avoid overwriting
        for (int sum = sums; sum >= nums[i]; sum--) {
            dp[sum] = dp[sum] || dp[sum - nums[i]];
        }
    }

    // The result is whether it's possible to make a subset with the sum equal to 'sums'
    return dp[sums];
}
```