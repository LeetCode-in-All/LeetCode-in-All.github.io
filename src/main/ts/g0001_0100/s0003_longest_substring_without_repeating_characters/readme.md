[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 3\. Longest Substring Without Repeating Characters

Medium

Given a string `s`, find the length of the **longest** **substring** without repeating characters.

**Example 1:**

**Input:** s = "abcabcbb"

**Output:** 3

**Explanation:** The answer is "abc", with the length of 3. 

**Example 2:**

**Input:** s = "bbbbb"

**Output:** 1

**Explanation:** The answer is "b", with the length of 1. 

**Example 3:**

**Input:** s = "pwwkew"

**Output:** 3

**Explanation:**

The answer is "wke", with the length of 3.

Notice that the answer must be a substring, "pwke" is a subsequence and not a substring. 

**Constraints:**

*   <code>0 <= s.length <= 5 * 10<sup>4</sup></code>
*   `s` consists of English letters, digits, symbols and spaces.

## Solution

```typescript
function lengthOfLongestSubstring(s: string): number {
    const lastIndices: number[] = new Array(256).fill(-1)
    let maxLen: number = 0
    let curLen: number = 0
    let start: number = 0
    for (let i = 0; i < s.length; i++) {
        const cur: string = s.charAt(i)
        const charCode: number = cur.charCodeAt(0)
        if (lastIndices[charCode] < start) {
            lastIndices[charCode] = i
            curLen++
        } else {
            const lastIndex: number = lastIndices[charCode]
            start = lastIndex + 1
            curLen = i - start + 1
            lastIndices[charCode] = i
        }
        if (curLen > maxLen) {
            maxLen = curLen
        }
    }
    return maxLen
}

export { lengthOfLongestSubstring }
```