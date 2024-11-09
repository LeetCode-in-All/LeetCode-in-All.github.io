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

```c
#include <stdbool.h>
#include <string.h>
#include <string.h>

bool isValid(char *s) {
    int n = strlen(s);
    if (n % 2 != 0) return false; // Check for odd length

    int i = 0;
    while (i < n - 1) {
        if ((s[i] == '(' && s[i + 1] == ')') ||
            (s[i] == '{' && s[i + 1] == '}') ||
            (s[i] == '[' && s[i + 1] == ']')) {
            // Remove matched parentheses
            memmove(&s[i], &s[i + 2], n - i - 1);
            n -= 2;
            s[n] = '\0';
            if (i >= 1) i--;
        } else {
            i++;
        }
    }

    return n == 0;
}
```