[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 34\. Find First and Last Position of Element in Sorted Array

Medium

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [5,7,7,8,8,10], target = 8

**Output:** [3,4]

**Example 2:**

**Input:** nums = [5,7,7,8,8,10], target = 6

**Output:** [-1,-1]

**Example 3:**

**Input:** nums = [], target = 0

**Output:** [-1,-1]

**Constraints:**

*   <code>0 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
*   `nums` is a non-decreasing array.
*   <code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code>

## Solution

```rust
impl Solution {
    pub fn search_range(nums: Vec<i32>, target: i32) -> Vec<i32> {
        let mut ans = vec![-1, -1];
        ans[0] = Solution::helper(&nums, target, false);
        ans[1] = Solution::helper(&nums, target, true);
        ans
    }

    fn helper(nums: &[i32], target: i32, equals: bool) -> i32 {
        let (mut l, mut r) = (0, nums.len() as i32 - 1);
        let mut result = -1;
        while l <= r {
            let mid = l + (r - l) / 2;
            if nums[mid as usize] == target {
                result = mid;
            }
            if nums[mid as usize] < target || (nums[mid as usize] == target && equals) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        result
    }
}
```