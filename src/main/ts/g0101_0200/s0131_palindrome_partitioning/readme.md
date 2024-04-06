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

```typescript
function partition(s: string): string[][] {
    const ans: string[][] = []
    const memo = Array.from({ length: s.length }).map(() => new Array(s.length))
    const track = (cur, start) => {
        if (start === s.length) {
            ans.push(cur.slice())
            return
        }
        for (let i = start; i < s.length; i++) {
            if (memo[start][i]) continue

            if (isPalindrome(s, start, i, memo)) {
                cur.push(s.substring(start, i + 1))
                track(cur, i + 1)
                cur.pop()
            }
        }
    }
    track([], 0)
    return ans
}

function isPalindrome(str: string, l: number, r: number, memo: boolean[][]) {
    while (l < r) {
        if (str[l] !== str[r]) {
            memo[l][r] = true
            return false
        }
        l++
        r--
    }
    return true
}

export { partition }
```