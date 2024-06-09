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

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        ans = []
        self._generate([], ans, n, n)
        return ans

    def _generate(self, current, result, open, close):
        if open == 0 and close == 0:
            result.append("".join(current))
            return
        if open > 0:
            current.append('(')
            self._generate(current, result, open - 1, close)
            current.pop()
        if close > 0 and open < close:
            current.append(')')
            self._generate(current, result, open, close - 1)
            current.pop()
```