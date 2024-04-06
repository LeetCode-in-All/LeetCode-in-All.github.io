[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 32\. Longest Valid Parentheses

Hard

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

**Example 1:**

**Input:** s = "(()"

**Output:** 2

**Explanation:** The longest valid parentheses substring is "()".

**Example 2:**

**Input:** s = ")()())"

**Output:** 4

**Explanation:** The longest valid parentheses substring is "()()".

**Example 3:**

**Input:** s = ""

**Output:** 0

**Constraints:**

-   <code>0 <= s.length <= 3 \* 10<sup>4</sup></code>
-   `s[i]` is `'('`, or `')'`.

## Solution

```typescript
function longestValidParentheses(s: string): number {
    let open = 0
    let close = 0
    let max = 0
    for (let char of s) {
        if (char === '(') {
            open++
        } else {
            close++
        }
        if (open === close) {
            max = Math.max(max, open + close)
        } else if (close > open) {
            open = 0
            close = 0
        }
    }
    open = 0
    close = 0
    for (let i = s.length - 1; i >= 0; i--) {
        if (s[i] === '(') {
            open++
        } else {
            close++
        }
        if (open === close) {
            max = Math.max(max, open + close)
        } else if (open > close) {
            open = 0
            close = 0
        }
    }
    return max
}

export { longestValidParentheses }
```