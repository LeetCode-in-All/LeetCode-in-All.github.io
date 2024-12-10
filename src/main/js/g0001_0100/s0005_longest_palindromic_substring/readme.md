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

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function (s) {
    // Create the transformed string with '#' characters
    const newStr = new Array(s.length * 2 + 1).fill('#')
    for (let i = 0; i < s.length; i++) {
        newStr[2 * i + 1] = s[i]
    }

    const dp = new Array(newStr.length).fill(0) // Array to store radius of palindromes
    let friendCenter = 0 // Center of the current known palindrome
    let friendRadius = 0 // Radius of the current known palindrome
    let lpsCenter = 0 // Center of the longest palindrome
    let lpsRadius = 0 // Radius of the longest palindrome

    for (let i = 0; i < newStr.length; i++) {
        // Calculate initial radius
        dp[i] =
            friendCenter + friendRadius > i ? Math.min(dp[2 * friendCenter - i], friendCenter + friendRadius - i) : 1

        // Expand the palindrome around the current center
        while (i + dp[i] < newStr.length && i - dp[i] >= 0 && newStr[i + dp[i]] === newStr[i - dp[i]]) {
            dp[i]++
        }

        // Update the friend palindrome if needed
        if (friendCenter + friendRadius < i + dp[i]) {
            friendCenter = i
            friendRadius = dp[i]
        }

        // Update the longest palindrome if needed
        if (lpsRadius < dp[i]) {
            lpsCenter = i
            lpsRadius = dp[i]
        }
    }

    // Extract the longest palindrome substring
    const start = Math.floor((lpsCenter - lpsRadius + 1) / 2)
    const end = Math.floor((lpsCenter + lpsRadius - 1) / 2)
    return s.substring(start, end)
}

export { longestPalindrome }
```