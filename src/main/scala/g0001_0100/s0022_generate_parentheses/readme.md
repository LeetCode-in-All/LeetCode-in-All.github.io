[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 22\. Generate Parentheses

Medium

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3

**Output:** ["((()))","(()())","(())()","()(())","()()()"] 

**Example 2:**

**Input:** n = 1

**Output:** ["()"] 

**Constraints:**

*   `1 <= n <= 8`

## Solution

```scala
import scala.collection.mutable.ListBuffer

object Solution {
    def generateParenthesis(n: Int): List[String] = {
        val sb = new StringBuilder()
        val ans = ListBuffer[String]()
        generate(sb, ans, n, n).toList
    }

    private def generate(sb: StringBuilder, str: ListBuffer[String], open: Int, close: Int): ListBuffer[String] = {
        if (open == 0 && close == 0) {
            str += sb.toString()
            return str
        }
        if (open > 0) {
            sb.append('(')
            generate(sb, str, open - 1, close)
            sb.deleteCharAt(sb.length - 1)
        }
        if (close > 0 && open < close) {
            sb.append(')')
            generate(sb, str, open, close - 1)
            sb.deleteCharAt(sb.length - 1)
        }
        str
    }
}
```