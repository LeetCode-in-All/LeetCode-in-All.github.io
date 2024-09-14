[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 46\. Permutations

Medium

Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

**Example 2:**

**Input:** nums = [0,1]

**Output:** [[0,1],[1,0]]

**Example 3:**

**Input:** nums = [1]

**Output:** [[1]]

**Constraints:**

*   `1 <= nums.length <= 6`
*   `-10 <= nums[i] <= 10`
*   All the integers of `nums` are **unique**.

## Solution

```rust
impl Solution {
    pub fn permute(nums: Vec<i32>) -> Vec<Vec<i32>> {
        if nums.is_empty() {
            return vec![];
        }

        let mut final_result = Vec::new();
        let mut curr_result = Vec::new();
        let mut used = vec![false; nums.len()];

        Solution::permute_recur(&nums, &mut final_result, &mut curr_result, &mut used);
        final_result
    }

    fn permute_recur(
        nums: &[i32],
        final_result: &mut Vec<Vec<i32>>,
        curr_result: &mut Vec<i32>,
        used: &mut Vec<bool>,
    ) {
        if curr_result.len() == nums.len() {
            final_result.push(curr_result.clone());
            return;
        }

        for i in 0..nums.len() {
            if used[i] {
                continue;
            }

            curr_result.push(nums[i]);
            used[i] = true;

            Solution::permute_recur(nums, final_result, curr_result, used);

            used[i] = false;
            curr_result.pop();
        }
    }
}
```