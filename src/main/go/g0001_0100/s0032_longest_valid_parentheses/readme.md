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

*   <code>0 <= s.length <= 3 * 10<sup>4</sup></code>
*   `s[i]` is `'('`, or `')'`.

## Solution

```golang
func longestValidParentheses(s string) int {
	max := 0
	left, right := 0, 0
	n := len(s)
	for i := 0; i < n; i++ {
		ch := s[i]
		if ch == '(' {
			left++
		} else {
			right++
		}
		if right > left {
			left, right = 0, 0
		}
		if left == right {
			max = maxInt(max, left+right)
		}
	}
	left, right = 0, 0
	for i := n - 1; i >= 0; i-- {
		ch := s[i]
		if ch == '(' {
			left++
		} else {
			right++
		}
		if left > right {
			left, right = 0, 0
		}
		if left == right {
			max = maxInt(max, left+right)
		}
	}
	return max
}

func maxInt(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```