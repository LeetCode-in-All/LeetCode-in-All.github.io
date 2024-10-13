[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 152\. Maximum Product Subarray

Medium

Given an integer array `nums`, find a contiguous non-empty subarray within the array that has the largest product, and return _the product_.

The test cases are generated so that the answer will fit in a **32-bit** integer.

A **subarray** is a contiguous subsequence of the array.

**Example 1:**

**Input:** nums = [2,3,-2,4]

**Output:** 6

**Explanation:** [2,3] has the largest product 6.

**Example 2:**

**Input:** nums = [-2,0,-1]

**Output:** 0

**Explanation:** The result cannot be 2, because [-2,-1] is not a subarray.

**Constraints:**

*   <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
*   `-10 <= nums[i] <= 10`
*   The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

## Solution

```dart
import 'dart:math';

class Solution {
  int maxProduct(List<int> nums) {
    /*
      m = max 
      l = left 
      r = right
      s = size
      */
    var m = nums.first;
    var l = 1;
    var r = 1;
    var s = nums.length;
    var last = s - 1;
    for (var i = 0; i < s; i++) {
      l *= nums[i];
      r *= nums[last - i];
      m = max(m, l);
      m = max(m, r);
      l = l == 0 ? 1 : l;
      r = r == 0 ? 1 : r;
    }
    return m;
  }
}
```