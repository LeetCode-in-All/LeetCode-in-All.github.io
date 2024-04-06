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

```scala
import scala.collection.mutable

object Solution {
    def topKFrequent(nums: Array[Int], k: Int): Array[Int] = {
        val freqMap = mutable.HashMap.empty[Int, Int]
        for (n <- nums) {
            freqMap.put(n, freqMap.getOrElse(n, 0) + 1)
        }
        val bucket = new Array[List[Int]](nums.length + 1)
        for ((key, freq) <- freqMap) {
            Option(bucket(freq)) match {
                case Some(value) => bucket.update(freq, key :: value)
                case None => bucket.update(freq, List(key))
            }
        }
        val res = new Array[Int](k)
        var counter = 0
        var pos = bucket.length - 1
        while (pos >= 0 && counter < k) {
            if (bucket(pos) != null) {
                for (integer <- bucket(pos)) {
                    res(counter) = integer
                    counter += 1
                }
            }
            pos -= 1
        }
        res
    }
}
```