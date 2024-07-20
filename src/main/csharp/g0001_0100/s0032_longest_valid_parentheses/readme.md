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

```csharp
public class Solution {
    public int LongestValidParentheses(string s) {
        int max = 0;
        int left = 0;
        int right = 0;
        int n = s.Length;
        char ch;
        for (int i = 0; i < n; i++) {
            ch = s[i];
            if (ch == '(') {
                left++;
            } else {
                right++;
            }
            if (right > left) {
                left = 0;
                right = 0;
            }
            if (left == right) {
                max = Math.Max(max, 2 * right);
            }
        }
        left = 0;
        right = 0;
        for (int i = n - 1; i >= 0; i--) {
            ch = s[i];
            if (ch == '(') {
                left++;
            } else {
                right++;
            }
            if (left > right) {
                left = 0;
                right = 0;
            }
            if (left == right) {
                max = Math.Max(max, 2 * left);
            }
        }
        return max;
    }
}
```