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

```rust
impl Solution {
    pub fn jump(nums: Vec<i32>) -> i32 {
        let mut length = 0;
        let mut max_length = 0;
        let mut min_jump = 0;

        for i in 0..(nums.len() - 1) {
            length -= 1;
            max_length -= 1;
            max_length = max_length.max(nums[i]);

            if length <= 0 {
                length = max_length;
                min_jump += 1;
            }

            if length >= (nums.len() - i - 1) as i32 {
                return min_jump;
            }
        }

        min_jump
    }
}
```