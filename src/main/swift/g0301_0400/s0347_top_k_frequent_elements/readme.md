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

```swift
import HeapModule

class Solution {
    func topKFrequent(_ nums: [Int], _ k: Int) -> [Int] {
        struct FreqElement: Comparable {
            let val: Int
            let freq: Int

            static func < (lhs: FreqElement, rhs: FreqElement) -> Bool {
                lhs.freq < rhs.freq
            }

            static func == (lhs: FreqElement, rhs: FreqElement) -> Bool {
                lhs.freq == rhs.freq
            }
        }
        var freqMap = [Int: Int]()
        for num in nums {
            freqMap[num, default: 0] += 1
        }
        var freqHeap = Heap<FreqElement>()
        for (key, value) in freqMap {
            freqHeap.insert(.init(val: key, freq: value))
            if freqHeap.count > k {
                freqHeap.removeMin()
            }
        }
        var res = [Int]()
        while let element = freqHeap.popMax() {
            res.append(element.val)
        }
        return res
    }
}
```