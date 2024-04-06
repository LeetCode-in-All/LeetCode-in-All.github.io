[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 76\. Minimum Window Substring

Hard

Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window substring** of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window. If there is no such substring__, return the empty string_ `""`_._

The testcases will be generated such that the answer is **unique**.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "ADOBECODEBANC", t = "ABC"

**Output:** "BANC"

**Explanation:** The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t. 

**Example 2:**

**Input:** s = "a", t = "a"

**Output:** "a"

**Explanation:** The entire string s is the minimum window. 

**Example 3:**

**Input:** s = "a", t = "aa"

**Output:** ""

**Explanation:** Both 'a's from t must be included in the window. Since the largest window of s only has one 'a', return empty string. 

**Constraints:**

*   `m == s.length`
*   `n == t.length`
*   <code>1 <= m, n <= 10<sup>5</sup></code>
*   `s` and `t` consist of uppercase and lowercase English letters.

**Follow up:** Could you find an algorithm that runs in `O(m + n)` time?

## Solution

```typescript
function minWindow(s: string, t: string): string { //NOSONAR
    const map: Map<string, number> = new Map()
    for (const char of t) {
        if (map.has(char)) {
            map.set(char, map.get(char) + 1)
        } else {
            map.set(char, 1)
        }
    }
    let minStartIdx = -Infinity,
        minEndIdx = Infinity
    let remainingChars = t.length
    let startIdx = 0
    for (let endIdx = 0; endIdx < s.length; endIdx++) {
        const endChar = s[endIdx]
        if (map.has(endChar)) {
            map.set(endChar, map.get(endChar) - 1)
            if (map.get(endChar) >= 0) {
                remainingChars--
            }
        }
        while (remainingChars === 0) {
            if (minEndIdx - minStartIdx > endIdx - startIdx) {
                minStartIdx = startIdx
                minEndIdx = endIdx
            }
            const startChar = s[startIdx]
            if (map.has(startChar)) {
                map.set(startChar, map.get(startChar) + 1)
            }
            if (map.get(startChar) > 0) {
                remainingChars++
            }
            startIdx++
        }
    }
    return minStartIdx === -Infinity ? '' : s.slice(minStartIdx, minEndIdx + 1)
}

export { minWindow }
```