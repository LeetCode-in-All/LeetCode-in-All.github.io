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

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        # Create a new string with separators
        new_str = ['#'] * (2 * len(s) + 1)
        for i in range(len(s)):
            new_str[2 * i + 1] = s[i]

        dp = [0] * len(new_str)
        friend_center = 0
        friend_radius = 0
        lps_center = 0
        lps_radius = 0

        for i in range(len(new_str)):
            if friend_center + friend_radius > i:
                dp[i] = min(dp[2 * friend_center - i], (friend_center + friend_radius) - i)
            else:
                dp[i] = 1

            while i + dp[i] < len(new_str) and i - dp[i] >= 0 and new_str[i + dp[i]] == new_str[i - dp[i]]:
                dp[i] += 1

            if friend_center + friend_radius < i + dp[i]:
                friend_center = i
                friend_radius = dp[i]

            if lps_radius < dp[i]:
                lps_center = i
                lps_radius = dp[i]

        start = (lps_center - lps_radius + 1) // 2
        end = (lps_center + lps_radius - 1) // 2
        return s[start:end]
```