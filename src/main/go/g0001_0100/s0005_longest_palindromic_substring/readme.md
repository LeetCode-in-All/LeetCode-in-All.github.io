[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 5\. Longest Palindromic Substring

Medium

Given a string `s`, return _the longest_ _palindromic_ _substring_ in `s`.

**Example 1:**

**Input:** s = "babad"

**Output:** "bab"

**Explanation:** "aba" is also a valid answer. 

**Example 2:**

**Input:** s = "cbbd"

**Output:** "bb" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consist of only digits and English letters.

## Solution

```golang
func longestPalindrome(s string) string {
	newStr := make([]byte, len(s)*2+1)
	newStr[0] = '#'
	for i := 0; i < len(s); i++ {
		newStr[2*i+1] = s[i]
		newStr[2*i+2] = '#'
	}
	dp := make([]int, len(newStr))
	friendCenter, friendRadius := 0, 0
	lpsCenter, lpsRadius := 0, 0
	for i := 0; i < len(newStr); i++ {
		if friendCenter+friendRadius > i {
			dp[i] = min(dp[2*friendCenter-i], (friendCenter+friendRadius)-i)
		} else {
			dp[i] = 1
		}
		for i+dp[i] < len(newStr) && i-dp[i] >= 0 && newStr[i+dp[i]] == newStr[i-dp[i]] {
			dp[i]++
		}
		if friendCenter+friendRadius < i+dp[i] {
			friendCenter, friendRadius = i, dp[i]
		}
		if lpsRadius < dp[i] {
			lpsCenter, lpsRadius = i, dp[i]
		}
	}
	return s[(lpsCenter-lpsRadius+1)/2 : (lpsCenter+lpsRadius-1)/2]
}

func min(a, b int) int {
	if a < b {
		return a
	}
	return b
}
```