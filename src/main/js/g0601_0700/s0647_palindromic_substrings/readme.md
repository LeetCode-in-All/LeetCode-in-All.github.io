[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 647\. Palindromic Substrings

Medium

Given a string `s`, return _the number of **palindromic substrings** in it_.

A string is a **palindrome** when it reads the same backward as forward.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "abc"

**Output:** 3

**Explanation:** Three palindromic strings: "a", "b", "c".

**Example 2:**

**Input:** s = "aaa"

**Output:** 6

**Explanation:** Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consists of lowercase English letters.

## Solution

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var countSubstrings = function(s) {
    const expand = (a, l, r, res) => {
        while (l >= 0 && r < a.length) {
            if (a[l] !== a[r]) {
                return
            } else {
                res.count++
                l--
                r++
            }
        }
    }

    const a = s.split('')
    const res = { count: 0 }

    for (let i = 0; i < a.length; i++) {
        expand(a, i, i, res)
        expand(a, i, i + 1, res)
    }

    return res.count
};

export { countSubstrings }
```