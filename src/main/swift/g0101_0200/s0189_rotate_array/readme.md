[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 189\. Rotate Array

Medium

Given an array, rotate the array to the right by `k` steps, where `k` is non-negative.

**Example 1:**

**Input:** nums = [1,2,3,4,5,6,7], k = 3

**Output:** [5,6,7,1,2,3,4]

**Explanation:**

    rotate 1 steps to the right: [7,1,2,3,4,5,6]
    rotate 2 steps to the right: [6,7,1,2,3,4,5]
    rotate 3 steps to the right: [5,6,7,1,2,3,4] 

**Example 2:**

**Input:** nums = [-1,-100,3,99], k = 2

**Output:** [3,99,-1,-100]

**Explanation:**

    rotate 1 steps to the right: [99,-1,-100,3]
    rotate 2 steps to the right: [3,99,-1,-100] 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>
*   <code>0 <= k <= 10<sup>5</sup></code>

**Follow up:**

*   Try to come up with as many solutions as you can. There are at least **three** different ways to solve this problem.
*   Could you do it in-place with `O(1)` extra space?

## Solution

```swift
class Solution {
    func rotate(_ nums: inout [Int], _ k: Int) {
        guard nums.count > 1, k > 0, k != nums.count else {
            return
        }

        let requiredRotationsCount = k % nums.count
        let pivotIndex = nums.count - requiredRotationsCount

        reverse(&nums, startIndex: nums.startIndex, endIndex: nums.endIndex - 1)
        reverse(&nums, startIndex: nums.startIndex, endIndex: requiredRotationsCount - 1)
        reverse(&nums, startIndex: requiredRotationsCount, endIndex: nums.endIndex - 1)

    }

    func reverse(_ nums: inout [Int], startIndex: Int, endIndex: Int) {
        var startIndex = startIndex
        var endIndex = endIndex

        while endIndex > startIndex {
            let temp = nums[startIndex]
            nums[startIndex] = nums[endIndex]
            nums[endIndex] = temp
            startIndex += 1
            endIndex -= 1
        }
    }
}
```