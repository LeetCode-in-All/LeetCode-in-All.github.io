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

```ruby
# @param {Integer} n
# @return {String[]}
def generate_parenthesis(n)
  res = []
  gen(res, '', n, 0, 0)

  res
end

def gen(res, str, n, open_num, close_num)
  res << str if close_num == n

  gen(res, "#{str})", n, open_num, close_num + 1) if close_num < open_num
  gen(res, "#{str}(", n, open_num + 1, close_num) if open_num < n
end
```