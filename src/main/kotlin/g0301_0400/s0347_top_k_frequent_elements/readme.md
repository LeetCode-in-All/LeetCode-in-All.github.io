[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 347\. Top K Frequent Elements

Medium

Given an integer array `nums` and an integer `k`, return _the_ `k` _most frequent elements_. You may return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,1,1,2,2,3], k = 2

**Output:** [1,2]

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1]

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   `k` is in the range `[1, the number of unique elements in the array]`.
*   It is **guaranteed** that the answer is **unique**.

**Follow up:** Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.

## Solution

```kotlin
import java.util.PriorityQueue
import java.util.Queue

@Suppress("kotlin:S6518")
class Solution {
    fun topKFrequent(nums: IntArray, k: Int): IntArray {
        nums.sort()
        // Min heap of <number, frequency>
        val queue: Queue<IntArray> = PriorityQueue(k + 1) { a: IntArray, b: IntArray -> a[1] - b[1] }
        // Filter with min heap
        var j = 0
        for (i in 0..nums.size) {
            if (i == nums.size || nums[i] != nums[j]) {
                queue.offer(intArrayOf(nums[j], i - j))
                if (queue.size > k) {
                    queue.poll()
                }
                j = i
            }
        }
        // Convert to int array
        val result = IntArray(k)
        for (i in k - 1 downTo 0) {
            result[i] = queue.poll().get(0)
        }
        return result
    }
}
```