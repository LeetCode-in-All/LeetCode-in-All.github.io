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

```scala
object Solution {
    @SuppressWarnings(Array("scala:S3776"))
    def longestValidParentheses(s: String): Int = {
        var max = 0
        var left = 0
        var right = 0
        val n = s.length

        for (i <- 0 until n) {
            val ch = s.charAt(i)
            if (ch == '(') {
                left += 1
            } else {
                right += 1
            }
            if (right > left) {
                left = 0
                right = 0
            }
            if (left == right) {
                max = math.max(max, left + right)
            }
        }

        left = 0
        right = 0
        for (i <- n - 1 to 0 by -1) {
            val ch = s.charAt(i)
            if (ch == '(') {
                left += 1
            } else {
                right += 1
            }
            if (left > right) {
                left = 0
                right = 0
            }
            if (left == right) {
                max = math.max(max, left + right)
            }
        }

        max
    }
}
```