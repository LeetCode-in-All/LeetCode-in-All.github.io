[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 55\. Jump Game

Medium

You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` _if you can reach the last index, or_ `false` _otherwise_.

**Example 1:**

**Input:** nums = [2,3,1,1,4]

**Output:** true

**Explanation:** Jump 1 step from index 0 to 1, then 3 steps to the last index. 

**Example 2:**

**Input:** nums = [3,2,1,0,4]

**Output:** false

**Explanation:** You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index. 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   <code>0 <= nums[i] <= 10<sup>5</sup></code>

## Solution

```scala
object Solution {
    def canJump(nums: Array[Int]): Boolean = {
        val sz = nums.length
        // We set tmp to 1 so it won't break on the first iteration
        var tmp = 1
        var result = true // Variable to store the result

        for (i <- 0 until sz if result) {
            // We always deduct tmp for every iteration
            tmp -= 1
            if (tmp < 0) {
                // If from the previous iteration tmp is already 0, it will be < 0 here,
                // leading to a false value
                result = false
            } else {
                // We get the maximum value because this value is supposed to be our iterator. If both values are 0,
                // then the next iteration will return false.
                // We can stop the whole iteration with this condition. Without this condition, the code runs in 2ms (79.6%).
                // Adding this condition improves the performance to 1ms (100%)
                // because if the test case jump value is quite large, instead of just iterating, we can
                // just check using this condition.
                // Example: [10, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] -> we can just jump to the end without iterating the whole array.
                tmp = math.max(tmp, nums(i))
                if (i + tmp >= sz - 1) {
                    result = true
                }
            }
        }

        result
    }
}
```