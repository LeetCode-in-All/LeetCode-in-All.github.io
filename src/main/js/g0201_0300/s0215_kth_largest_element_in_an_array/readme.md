[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 215\. Kth Largest Element in an Array

Medium

Given an integer array `nums` and an integer `k`, return _the_ <code>k<sup>th</sup></code> _largest element in the array_.

Note that it is the <code>k<sup>th</sup></code> largest element in the sorted order, not the <code>k<sup>th</sup></code> distinct element.

You must solve it in `O(n)` time complexity.

**Example 1:**

**Input:** nums = [3,2,1,5,6,4], k = 2

**Output:** 5

**Example 2:**

**Input:** nums = [3,2,3,1,2,4,5,5,6], k = 4

**Output:** 4

**Constraints:**

*   <code>1 <= k <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

## Solution

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findKthLargest = function(nums, k) {
    const min = Math.min(...nums)
    const max = Math.max(...nums)
    const dp = new Array(max - min + 1).fill(0)
    for (let num of nums) {
        dp[num - min]++
    }
    for (let i = dp.length-1; i >= 0; i--) {
        k -= dp[i]
        if (k <= 0) return i + min
    }
};

export { findKthLargest }
```