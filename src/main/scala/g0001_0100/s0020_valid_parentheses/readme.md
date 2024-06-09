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

```scala
import scala.collection.mutable.Stack
import scala.util.control.Breaks._

object Solution {
    def isValid(s: String): Boolean = {
        val stack = Stack[Char]()
        var result = true

        breakable {
            for (i <- 0 until s.length) {
                val c = s.charAt(i)
                if (c == '(' || c == '[' || c == '{') {
                    stack.push(c)
                } else if (c == ')' && stack.nonEmpty && stack.top == '(') {
                    stack.pop()
                } else if (c == '}' && stack.nonEmpty && stack.top == '{') {
                    stack.pop()
                } else if (c == ']' && stack.nonEmpty && stack.top == '[') {
                    stack.pop()
                } else {
                    result = false
                    break()
                }
            }
        }

        result && stack.isEmpty
    }
}
```