[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 169\. Majority Element

Easy

Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**

**Input:** nums = [3,2,3]

**Output:** 3 

**Example 2:**

**Input:** nums = [2,2,1,1,1,2,2]

**Output:** 2 

**Constraints:**

*   `n == nums.length`
*   <code>1 <= n <= 5 * 10<sup>4</sup></code>
*   <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>

**Follow-up:** Could you solve the problem in linear time and in `O(1)` space?

## Solution

```swift
class Solution {
    func majorityElement(_ arr: [Int]) -> Int {
        var count = 1
        var majority = arr[0]

        // For Potential Majority Element
        for i in 1..<arr.count {
            if arr[i] == majority {
                count += 1
            } else {
                if count > 1 {
                    count -= 1
                } else {
                    majority = arr[i]
                }
            }
        }

        // For Confirmation
        count = 0
        for num in arr {
            if num == majority {
                count += 1
            }
        }
        return count >= (arr.count / 2) + 1 ? majority : -1
    }
}
```