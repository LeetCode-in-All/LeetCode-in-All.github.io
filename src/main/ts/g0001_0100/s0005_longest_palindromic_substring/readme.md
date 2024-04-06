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

```typescript
function longestPalindrome(s: string): string {
    const newStr: string[] = new Array(s.length * 2 + 1)
    newStr[0] = '#'
    for (let i = 0; i < s.length; i++) {
        newStr[2 * i + 1] = s.charAt(i)
        newStr[2 * i + 2] = '#'
    }
    const dp: number[] = new Array(newStr.length)
    let friendCenter: number = 0
    let friendRadius: number = 0
    let lpsCenter: number = 0
    let lpsRadius: number = 0
    for (let i = 0; i < newStr.length; i++) {
        dp[i] =
            friendCenter + friendRadius > i ? Math.min(dp[2 * friendCenter - i], friendCenter + friendRadius - i) : 1
        while (i + dp[i] < newStr.length && i - dp[i] >= 0 && newStr[i + dp[i]] === newStr[i - dp[i]]) {
            dp[i]++
        }
        if (friendCenter + friendRadius < i + dp[i]) {
            friendCenter = i
            friendRadius = dp[i]
        }
        if (lpsRadius < dp[i]) {
            lpsCenter = i
            lpsRadius = dp[i]
        }
    }
    return s.substring((lpsCenter - lpsRadius + 1) / 2, (lpsCenter + lpsRadius - 1) / 2)
}

export { longestPalindrome }
```