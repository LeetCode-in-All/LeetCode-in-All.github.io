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

```rust
impl Solution {
    pub fn rotate(nums: &mut Vec<i32>, k: i32) {
        let mut rotated = vec![0; nums.len()];
        let k_fixed = k as usize % nums.len();

        for (i, item) in nums.iter().enumerate() {
            match nums.get(i+k_fixed) {
                Some(n) => rotated[i+k_fixed] = *item,
                None => rotated[(i+k_fixed)-nums.len()] = *item,
            }
        }
        nums.copy_from_slice(&rotated)
    }
}
```