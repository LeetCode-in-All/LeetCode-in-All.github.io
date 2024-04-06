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

```typescript
function generateParenthesis(n: number): string[] {
    const sb: string[] = []
    const ans: string[] = []
    return generate(sb, ans, n, n)
}

function generate(sb: string[], str: string[], open: number, close: number): string[] {
    if (open === 0 && close === 0) {
        str.push(sb.join(''))
        return str
    }
    if (open > 0) {
        sb.push('(')
        generate(sb, str, open - 1, close)
        sb.pop()
    }
    if (close > 0 && open < close) {
        sb.push(')')
        generate(sb, str, open, close - 1)
        sb.pop()
    }
    return str
}

export { generateParenthesis }
```