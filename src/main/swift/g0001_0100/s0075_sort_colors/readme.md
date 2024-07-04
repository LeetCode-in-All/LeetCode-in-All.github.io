[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 75\. Sort Colors

Medium

Given an array `nums` with `n` objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

**Example 1:**

**Input:** nums = [2,0,2,1,1,0]

**Output:** [0,0,1,1,2,2] 

**Example 2:**

**Input:** nums = [2,0,1]

**Output:** [0,1,2] 

**Example 3:**

**Input:** nums = [0]

**Output:** [0] 

**Example 4:**

**Input:** nums = [1]

**Output:** [1] 

**Constraints:**

*   `n == nums.length`
*   `1 <= n <= 300`
*   `nums[i]` is `0`, `1`, or `2`.

**Follow up:** Could you come up with a one-pass algorithm using only constant extra space?

To solve the "Sort Colors" problem in Swift with the Solution class, follow these steps:

1. Define a method `sortColors` in the `Solution` class that takes an array of integers `nums` as input and sorts it in-place according to the colors red, white, and blue.
2. Initialize three pointers: `low`, `mid`, and `high`. `low` points to the beginning of the array, `mid` points to the current element being processed, and `high` points to the end of the array.
3. Loop while `mid` is less than or equal to `high`:
   - If `nums[mid]` is 0, swap `nums[low]` with `nums[mid]`, increment `low` and `mid`.
   - If `nums[mid]` is 1, increment `mid`.
   - If `nums[mid]` is 2, swap `nums[mid]` with `nums[high]`, decrement `high`.
4. After the loop, the array will be sorted in-place according to the colors red, white, and blue.

Here's the implementation of the `sortColors` method in Swift:

```swift
class Solution {
    func sortColors(_ nums: inout [Int]) {
        var zeroes = 0
        var ones = 0
        
        for i in 0..<nums.count {
            if nums[i] == 0 {
                nums[zeroes] = 0
                zeroes += 1
            } else if nums[i] == 1 {
                ones += 1
            }
        }
        
        for j in zeroes..<(zeroes + ones) {
            nums[j] = 1
        }
        
        for k in (zeroes + ones)..<nums.count {
            nums[k] = 2
        }
    }
}
```

This implementation sorts the array in-place using a one-pass algorithm with constant extra space. It iterates through the array and swaps elements as needed to group them according to their colors. The time complexity of this solution is O(n), where n is the length of the array.