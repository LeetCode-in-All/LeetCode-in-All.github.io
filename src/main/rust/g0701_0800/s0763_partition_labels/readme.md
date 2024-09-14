[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 763\. Partition Labels

Medium

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return _a list of integers representing the size of these parts_.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"

**Output:** [9,7,8]

**Explanation:** The partition is "ababcbaca", "defegde", "hijhklij". This is a partition so that each letter appears in at most one part. A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.

**Example 2:**

**Input:** s = "eccbbbbdec"

**Output:** [10]

**Constraints:**

*   `1 <= s.length <= 500`
*   `s` consists of lowercase English letters.

## Solution

```rust
impl Solution {
    pub fn partition_labels(s: String) -> Vec<i32> {
        let letters: Vec<char> = s.chars().collect();
        let mut result = Vec::new();
        let mut position = vec![0; 26];

        // Store the last occurrence of each letter in the string
        for (i, &ch) in letters.iter().enumerate() {
            position[(ch as usize) - ('a' as usize)] = i;
        }

        let mut i = 0;
        let mut prev = -1;
        let mut max = 0;

        // Iterate over the string to find partitions
        while i < letters.len() {
            let ch_pos = position[(letters[i] as usize) - ('a' as usize)];
            if ch_pos > max {
                max = ch_pos;
            }

            if i == max {
                result.push((i as i32) - (prev as i32));
                prev = i as i32;
            }

            i += 1;
        }

        result
    }
}
```