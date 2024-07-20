[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 20\. Valid Parentheses

Easy

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1.  Open brackets must be closed by the same type of brackets.
2.  Open brackets must be closed in the correct order.

**Example 1:**

**Input:** s = "()"

**Output:** true 

**Example 2:**

**Input:** s = "()[]{}"

**Output:** true 

**Example 3:**

**Input:** s = "(]"

**Output:** false 

**Example 4:**

**Input:** s = "([)]"

**Output:** false 

**Example 5:**

**Input:** s = "{[]}"

**Output:** true 

**Constraints:**

*   <code>1 <= s.length <= 10<sup>4</sup></code>
*   `s` consists of parentheses only `'()[]{}'`.

## Solution

```csharp
using System;
using System.Collections.Generic;

public class Solution {
    public bool IsValid(string s) {
        Stack<char> stack = new Stack<char>();
        for (int i = 0; i < s.Length; i++) {
            char c = s[i];
            if (c == '(' || c == '[' || c == '{') {
                stack.Push(c);
            } else if (c == ')' && stack.Count > 0 && stack.Peek() == '(') {
                stack.Pop();
            } else if (c == '}' && stack.Count > 0 && stack.Peek() == '{') {
                stack.Pop();
            } else if (c == ']' && stack.Count > 0 && stack.Peek() == '[') {
                stack.Pop();
            } else {
                return false;
            }
        }
        return stack.Count == 0;
    }
}
```