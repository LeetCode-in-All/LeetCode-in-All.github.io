[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 45\. Jump Game II

Medium

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

**Example 1:**

**Input:** nums = [2,3,1,1,4]

**Output:** 2

**Explanation:** The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index. 

**Example 2:**

**Input:** nums = [2,3,0,1,4]

**Output:** 2 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   `0 <= nums[i] <= 1000`

## Solution

```scala
object Solution {
    def jump(nums: Array[Int]): Int = {
        var length = 0
        var maxLength = 0
        var minJump = 0

        for (i <- 0 until nums.length - 1) {
            length -= 1
            maxLength -= 1
            maxLength = math.max(maxLength, nums(i))

            if (length <= 0) {
                length = maxLength
                minJump += 1
            }

            if (length >= nums.length - i - 1) {
                return minJump
            }
        }

        minJump
    }
}
```