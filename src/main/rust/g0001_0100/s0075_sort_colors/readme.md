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

**Constraints:**

*   `n == nums.length`
*   `1 <= n <= 300`
*   `nums[i]` is either `0`, `1`, or `2`.

**Follow up:** Could you come up with a one-pass algorithm using only constant extra space?

## Solution

```rust
impl Solution {
    pub fn sort_colors(nums: &mut Vec<i32>) {
        let mut zeroes = 0;
        let mut ones = 0;

        // First pass: Count and place all zeroes
        for i in 0..nums.len() {
            if nums[i] == 0 {
                nums[zeroes] = 0;
                zeroes += 1;
            } else if nums[i] == 1 {
                ones += 1;
            }
        }

        // Second pass: Place all ones
        for j in zeroes..(zeroes + ones) {
            nums[j] = 1;
        }

        // Third pass: Place all twos
        for k in (zeroes + ones)..nums.len() {
            nums[k] = 2;
        }
    }
}
```