[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 35\. Search Insert Position

Easy

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [1,3,5,6], target = 5

**Output:** 2

**Example 2:**

**Input:** nums = [1,3,5,6], target = 2

**Output:** 1

**Example 3:**

**Input:** nums = [1,3,5,6], target = 7

**Output:** 4

**Example 4:**

**Input:** nums = [1,3,5,6], target = 0

**Output:** 0

**Example 5:**

**Input:** nums = [1], target = 0

**Output:** 0

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `nums` contains **distinct** values sorted in **ascending** order.
*   <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>

## Solution

```kotlin
class Solution {
    fun searchInsert(nums: IntArray, target: Int): Int {
        var lo = 0
        var hi = nums.size - 1
        while (lo <= hi) {
            val mid = lo + (hi - lo) / 2
            if (target == nums[mid]) {
                return mid
            } else if (target < nums[mid]) {
                hi = mid - 1
            } else if (target > nums[mid]) {
                lo = mid + 1
            }
        }
        return lo
    }
}
```