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
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `k` is in the range `[1, the number of unique elements in the array]`.
*   It is **guaranteed** that the answer is **unique**.

**Follow up:** Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.

## Solution

```rust
use std::collections::HashMap;

impl Solution {
    pub fn top_k_frequent(nums: Vec<i32>, k: i32) -> Vec<i32> {
        nums.iter().fold(HashMap::new(), |mut map, n| {
            let mut counter = map.entry(n).or_insert(0);
            *counter += 1;
            map
        })
        .drain()
        .fold(vec![(0, 0); k as usize], |mut top_k, (&num, count)| {
            if count > top_k[0].1 {
                top_k[0] = (num, count);

                let mut next_index = 1;
                while next_index < k as usize {
                    if count > top_k[next_index].1 {
                        let temp = top_k[next_index];
                        top_k[next_index] = (num, count);
                        top_k[next_index - 1] = temp;
                    }
                    next_index += 1;
                }
            }

            top_k
        })
        .into_iter()
        .map(|(num, count)| num)
        .collect()
    }
}
```