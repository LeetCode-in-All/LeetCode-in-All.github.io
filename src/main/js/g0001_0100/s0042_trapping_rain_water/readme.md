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

```javascript
/**
 * @param {number[]} height
 * @return {number}
 */
var trap = function(height) {
    let l = 0
    let r = height.length - 1
    let res = 0
    let lowerWall = 0

    while (l < r) {
        let lVal = height[l]
        let rVal = height[r]

        if (lVal < rVal) {
            lowerWall = Math.max(lVal, lowerWall)
            res += lowerWall - lVal
            l++
        } else {
            lowerWall = Math.max(rVal, lowerWall)
            res += lowerWall - rVal
            r--
        }
    }

    return res
};

export { trap }
```