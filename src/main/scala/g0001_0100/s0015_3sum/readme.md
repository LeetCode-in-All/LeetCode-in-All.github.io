[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 15\. 3Sum

Medium

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

**Input:** nums = [-1,0,1,2,-1,-4]

**Output:** [[-1,-1,2],[-1,0,1]] 

**Example 2:**

**Input:** nums = []

**Output:** [] 

**Example 3:**

**Input:** nums = [0]

**Output:** [] 

**Constraints:**

*   `0 <= nums.length <= 3000`
*   <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>

## Solution

```scala
object Solution {
    @SuppressWarnings(Array("scala:S3776"))
    def threeSum(nums: Array[Int]): List[List[Int]] = {
        val sortedNums = nums.sorted
        var result: List[List[Int]] = List()
        for (i <- 0 until sortedNums.length - 2) {
            if (i == 0 || (i > 0 && sortedNums(i) != sortedNums(i - 1))) {
                var left = i + 1
                var right = sortedNums.length - 1
                val target = -sortedNums(i)
                while (left < right) {
                    if (sortedNums(left) + sortedNums(right) == target) {
                        result = List(sortedNums(i), sortedNums(left), sortedNums(right)) :: result
                        while (left < right && sortedNums(left) == sortedNums(left + 1))
                            left += 1
                        while (left < right && sortedNums(right) == sortedNums(right - 1))
                            right -= 1

                        left += 1
                        right -= 1
                    } else if (sortedNums(left) + sortedNums(right) < target)
                        left += 1
                    else
                        right -= 1
                }
            }
        }
        result
    }
}
```