[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 10\. Regular Expression Matching

Hard

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:

*   `'.'` Matches any single character.
*   `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

**Example 1:**

**Input:** s = "aa", p = "a"

**Output:** false

**Explanation:** "a" does not match the entire string "aa". 

**Example 2:**

**Input:** s = "aa", p = "a\*"

**Output:** true

**Explanation:** '\*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa". 

**Example 3:**

**Input:** s = "ab", p = ".\*"

**Output:** true

**Explanation:** ".\*" means "zero or more (\*) of any character (.)". 

**Example 4:**

**Input:** s = "aab", p = "c\*a\*b"

**Output:** true

**Explanation:** c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab". 

**Example 5:**

**Input:** s = "mississippi", p = "mis\*is\*p\*."

**Output:** false 

**Constraints:**

*   `1 <= s.length <= 20`
*   `1 <= p.length <= 30`
*   `s` contains only lowercase English letters.
*   `p` contains only lowercase English letters, `'.'`, and `'*'`.
*   It is guaranteed for each appearance of the character `'*'`, there will be a previous valid character to match.

## Solution

```typescript
function isMatch(s: string, p: string): boolean { // NOSONAR
    const result = new Array(s.length + 1)
    for (let i = 0; i < result.length; i++) {
        result[i] = new Array(p.length + 1).fill(false)
    }
    result[0][0] = true
    for (let j = 1; j < result[0].length; j++) {
        const pChar = p[j - 1]
        if (pChar === '*') {
            result[0][j] = result[0][j - 2]
        }
    }
    for (let i = 1; i < result.length; i++) {
        for (let j = 1; j < result[0].length; j++) {
            const sChar = s[i - 1]
            const pChar = p[j - 1]
            if (sChar === pChar || pChar === '.') {
                result[i][j] = result[i - 1][j - 1]
            } else if (pChar === '*') {
                const prevCharMatch = sChar === p[j - 2] || p[j - 2] === '.' ? result[i - 1][j] : false
                result[i][j] = result[i][j - 2] || prevCharMatch
            }
        }
    }
    return result[result.length - 1][result[0].length - 1]
}

export { isMatch }
```