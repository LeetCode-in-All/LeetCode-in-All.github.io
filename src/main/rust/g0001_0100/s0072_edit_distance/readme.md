[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 72\. Edit Distance

Hard

Given two strings `word1` and `word2`, return _the minimum number of operations required to convert `word1` to `word2`_.

You have the following three operations permitted on a word:

*   Insert a character
*   Delete a character
*   Replace a character

**Example 1:**

**Input:** word1 = "horse", word2 = "ros"

**Output:** 3

**Explanation:** 

horse -> rorse (replace 'h' with 'r') 

rorse -> rose (remove 'r') 

rose -> ros (remove 'e')

**Example 2:**

**Input:** word1 = "intention", word2 = "execution"

**Output:** 5

**Explanation:** 

intention -> inention (remove 't') 

inention -> enention (replace 'i' with 'e') 

enention -> exention (replace 'n' with 'x') 

exention -> exection (replace 'n' with 'c') 

exection -> execution (insert 'u')

**Constraints:**

*   `0 <= word1.length, word2.length <= 500`
*   `word1` and `word2` consist of lowercase English letters.

## Solution

```rust
impl Solution {
    pub fn min_distance(w1: String, w2: String) -> i32 {
        let n1 = w1.len();
        let n2 = w2.len();

        // Ensure the longer word is `w1`
        if n2 > n1 {
            return Solution::min_distance(w2, w1);
        }

        let w1_chars: Vec<char> = w1.chars().collect();
        let w2_chars: Vec<char> = w2.chars().collect();

        // Initialize dp array
        let mut dp = vec![0; n2 + 1];
        for j in 0..=n2 {
            dp[j] = j as i32;
        }

        // Dynamic programming to calculate minimum distance
        for i in 1..=n1 {
            let mut pre = dp[0];
            dp[0] = i as i32;

            for j in 1..=n2 {
                let tmp = dp[j];
                dp[j] = if w1_chars[i - 1] != w2_chars[j - 1] {
                    1 + i32::min(pre, i32::min(dp[j], dp[j - 1]))
                } else {
                    pre
                };
                pre = tmp;
            }
        }

        dp[n2]
    }
}
```