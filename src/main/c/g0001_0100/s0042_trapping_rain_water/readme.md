[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 42\. Trapping Rain Water

Hard

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

**Input:** height = [0,1,0,2,1,0,1,3,2,1,2,1]

**Output:** 6

**Explanation:** The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

**Example 2:**

**Input:** height = [4,2,0,3,2,5]

**Output:** 9

**Constraints:**

*   `n == height.length`
*   <code>1 <= n <= 2 * 10<sup>4</sup></code>
*   <code>0 <= height[i] <= 10<sup>5</sup></code>

## Solution

```c
#include <stdio.h>

int trap(int* height, int heightSize) {
    int l = 0;
    int r = heightSize - 1;
    int res = 0;
    int lowerWall = 0;

    while (l < r) {
        int lVal = height[l];
        int rVal = height[r];

        // Determine which side has the lower wall and add water accordingly
        if (lVal < rVal) {
            // Update lower wall height if lVal has increased
            lowerWall = lVal > lowerWall ? lVal : lowerWall;
            // Add the trapped water at this position
            res += lowerWall - lVal;
            // Move left pointer
            l++;
        } else {
            // Update lower wall height if rVal has increased
            lowerWall = rVal > lowerWall ? rVal : lowerWall;
            // Add the trapped water at this position
            res += lowerWall - rVal;
            // Move right pointer
            r--;
        }
    }

    return res;
}
```