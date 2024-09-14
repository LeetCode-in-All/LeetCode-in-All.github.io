[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 1\. Two Sum

Easy

Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

You may assume that each input would have **_exactly_ one solution**, and you may not use the _same_ element twice.

You can return the answer in any order.

**Example 1:**

**Input:** nums = [2,7,11,15], target = 9

**Output:** [0,1]

**Output:** Because nums[0] + nums[1] == 9, we return [0, 1]. 

**Example 2:**

**Input:** nums = [3,2,4], target = 6

**Output:** [1,2] 

**Example 3:**

**Input:** nums = [3,3], target = 6

**Output:** [0,1] 

**Constraints:**

*   <code>2 <= nums.length <= 10<sup>4</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
*   <code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code>
*   **Only one valid answer exists.**

**Follow-up:** Can you come up with an algorithm that is less than <code>O(n<sup>2</sup>) </code>time complexity?

## Solution

```rust
use std::collections::HashMap;

impl Solution {
    pub fn two_sum(numbers: Vec<i32>, target: i32) -> Vec<i32> {
        let mut index_map: HashMap<i32, usize> = HashMap::new();
        
        for (i, &num) in numbers.iter().enumerate() {
            let required_num = target - num;
            if let Some(&index) = index_map.get(&required_num) {
                return vec![index as i32, i as i32];
            }
            index_map.insert(num, i);
        }
        
        vec![-1, -1]
    }
}
```