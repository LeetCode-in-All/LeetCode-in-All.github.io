[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 70\. Climbing Stairs

Easy

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**

**Input:** n = 2

**Output:** 2

**Explanation:** There are two ways to climb to the top. 

1. 1 step + 1 step 

2. 2 steps

**Example 2:**

**Input:** n = 3

**Output:** 3

**Explanation:** There are three ways to climb to the top. 

1. 1 step + 1 step + 1 step 

2. 1 step + 2 steps 

3. 2 steps + 1 step

**Constraints:**

*   `1 <= n <= 45`

## Solution

```c
#include <stdio.h>
#include <stdlib.h>

int climbStairs(int n) {
    if (n < 2) {
        return n;
    }

    // Create an array to store the number of ways to climb to each step
    int* cache = (int*)malloc(n * sizeof(int));
    
    // Base cases
    cache[0] = 1; // 1 way to climb to the 1st step
    cache[1] = 2; // 2 ways to climb to the 2nd step

    // Fill the cache using dynamic programming
    for (int i = 2; i < n; i++) {
        cache[i] = cache[i - 1] + cache[i - 2];
    }

    // Store the result
    int result = cache[n - 1];

    // Free allocated memory
    free(cache);

    return result;
}
```