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

```rust
impl Solution {
    pub fn generate_parenthesis(n: i32) -> Vec<String> {
        let mut result = Vec::new();
        let mut current = String::new();
        Solution::generate(&mut current, &mut result, n, n);
        result
    }

    fn generate(current: &mut String, result: &mut Vec<String>, open: i32, close: i32) {
        if open == 0 && close == 0 {
            result.push(current.clone());
            return;
        }

        if open > 0 {
            current.push('(');
            Solution::generate(current, result, open - 1, close);
            current.pop();
        }

        if close > 0 && open < close {
            current.push(')');
            Solution::generate(current, result, open, close - 1);
            current.pop();
        }
    }
}
```