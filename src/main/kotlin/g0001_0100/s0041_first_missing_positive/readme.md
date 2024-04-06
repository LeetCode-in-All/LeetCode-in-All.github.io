[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 41\. First Missing Positive

Hard

Given an unsorted integer array `nums`, return the smallest missing positive integer.

You must implement an algorithm that runs in `O(n)` time and uses constant extra space.

**Example 1:**

**Input:** nums = [1,2,0]

**Output:** 3 

**Example 2:**

**Input:** nums = [3,4,-1,1]

**Output:** 2 

**Example 3:**

**Input:** nums = [7,8,9,11,12]

**Output:** 1 

**Constraints:**

*   <code>1 <= nums.length <= 5 * 10<sup>5</sup></code>
*   <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>

## Solution

```kotlin
class Solution {
    fun firstMissingPositive(nums: IntArray): Int {
        var noOne = true
        for (i in 0 until nums.size) {
            if (noOne && nums[i] == 1) {
                noOne = false
            } else if (nums[i] <= 0) {
                nums[i] = 1
            }
        }
        if (noOne) {
            return 1
        }
        var high = 0
        var k: Int
        for (x in nums) {
            k = kotlin.math.abs(x)
            high = kotlin.math.max(high, k)
            if (k - 1 < nums.size) {
                nums[k - 1] = -1 * kotlin.math.abs(nums[k - 1])
            }
        }
        for (i in nums.indices) {
            if (nums[i] > 0) {
                return i + 1
            }
        }
        return high + 1
    }
}
```