[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 5\. Longest Palindromic Substring

Medium

Given a string `s`, return _the longest palindromic substring_ in `s`.

**Example 1:**

**Input:** s = "babad"

**Output:** "bab" **Note:** "aba" is also a valid answer. 

**Example 2:**

**Input:** s = "cbbd"

**Output:** "bb" 

**Example 3:**

**Input:** s = "a"

**Output:** "a" 

**Example 4:**

**Input:** s = "ac"

**Output:** "a" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consist of only digits and English letters.

## Solution

```rust
impl Solution {
    pub fn longest_palindrome(s: String) -> String {
        let n = s.len();
        if n == 0 {
            return String::new();
        }

        // Step 1: Transform the string to avoid even/odd length issues
        let mut new_str = Vec::with_capacity(n * 2 + 1);
        new_str.push('#');
        for c in s.chars() {
            new_str.push(c);
            new_str.push('#');
        }

        let m = new_str.len();
        let mut dp = vec![0; m];
        let mut friend_center = 0;
        let mut friend_radius = 0;
        let mut lps_center = 0;
        let mut lps_radius = 0;

        // Step 2: Apply Manacher's Algorithm
        for i in 0..m {
            dp[i] = if friend_center + friend_radius > i {
                dp[2 * friend_center - i].min(friend_center + friend_radius - i)
            } else {
                1
            };

            while i + dp[i] < m && i >= dp[i] && new_str[i + dp[i]] == new_str[i - dp[i]] {
                dp[i] += 1;
            }

            if friend_center + friend_radius < i + dp[i] {
                friend_center = i;
                friend_radius = dp[i];
            }

            if lps_radius < dp[i] {
                lps_center = i;
                lps_radius = dp[i];
            }
        }

        // Step 3: Extract the longest palindromic substring
        let start = (lps_center - lps_radius + 1) / 2;
        let end = (lps_center + lps_radius - 1) / 2;
        s[start..end].to_string()
    }
}
```