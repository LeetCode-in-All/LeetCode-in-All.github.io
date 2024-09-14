[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 131\. Palindrome Partitioning

Medium

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

**Example 1:**

**Input:** s = "aab"

**Output:** [["a","a","b"],["aa","b"]]

**Example 2:**

**Input:** s = "a"

**Output:** [["a"]]

**Constraints:**

*   `1 <= s.length <= 16`
*   `s` contains only lowercase English letters.

## Solution

```rust
impl Solution {
    pub fn partition(s: String) -> Vec<Vec<String>> {
        let mut res = Vec::new();
        let mut curr_arr = Vec::new();
        Self::backtracking(&mut res, &mut curr_arr, &s, 0);
        res
    }

    fn backtracking(res: &mut Vec<Vec<String>>, curr_arr: &mut Vec<String>, s: &str, start: usize) {
        if start == s.len() {
            res.push(curr_arr.clone());
            return;
        }
        for end in start..s.len() {
            if !Self::is_palindrome(s, start, end) {
                continue;
            }
            curr_arr.push(s[start..=end].to_string());
            Self::backtracking(res, curr_arr, s, end + 1);
            curr_arr.pop();
        }
    }

    fn is_palindrome(s: &str, mut start: usize, mut end: usize) -> bool {
        while start < end && s.as_bytes()[start] == s.as_bytes()[end] {
            start += 1;
            end -= 1;
        }
        start >= end
    }
}
```