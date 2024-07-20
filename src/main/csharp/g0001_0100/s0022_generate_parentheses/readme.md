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

```csharp
using System.Collections.Generic;
using System.Text;

public class Solution {
    public IList<string> GenerateParenthesis(int n) {
        StringBuilder sb = new StringBuilder();
        List<string> ans = new List<string>();
        return Generate(sb, ans, n, n);
    }

    private IList<string> Generate(StringBuilder sb, List<string> str, int open, int close) {
        if (open == 0 && close == 0) {
            str.Add(sb.ToString());
            return str;
        }
        if (open > 0) {
            sb.Append('(');
            Generate(sb, str, open - 1, close);
            sb.Length--; // Equivalent to deleting the last character in StringBuilder
        }
        if (close > 0 && open < close) {
            sb.Append(')');
            Generate(sb, str, open, close - 1);
            sb.Length--; // Equivalent to deleting the last character in StringBuilder
        }
        return str;
    }
}
```