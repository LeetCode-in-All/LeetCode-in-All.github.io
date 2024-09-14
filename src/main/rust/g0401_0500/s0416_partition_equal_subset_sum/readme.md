[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 416\. Partition Equal Subset Sum

Medium

Given a **non-empty** array `nums` containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Example 1:**

**Input:** nums = [1,5,11,5]

**Output:** true

**Explanation:** The array can be partitioned as [1, 5, 5] and [11].

**Example 2:**

**Input:** nums = [1,2,3,5]

**Output:** false

**Explanation:** The array cannot be partitioned into equal sum subsets.

**Constraints:**

*   `1 <= nums.length <= 200`
*   `1 <= nums[i] <= 100`

## Solution

```rust
impl Solution {
    pub fn can_partition(nums: Vec<i32>) -> bool {
        let mut sums: i32 = nums.iter().sum();
        
        if sums % 2 != 0 {
            return false;
        }
        
        sums /= 2;
        let mut dp = vec![false; (sums + 1) as usize];
        dp[0] = true;
        
        for &num in &nums {
            for sum in (num..=sums).rev() {
                dp[sum as usize] = dp[sum as usize] || dp[(sum - num) as usize];
            }
        }
        
        dp[sums as usize]
    }
}
```