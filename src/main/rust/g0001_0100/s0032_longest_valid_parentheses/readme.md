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

```rust
impl Solution {
    pub fn longest_valid_parentheses(s: String) -> i32 {
        let mut max_len = 0;
        let mut left = 0;
        let mut right = 0;
        let n = s.len();
        let chars: Vec<char> = s.chars().collect();

        // Left to right pass
        for i in 0..n {
            if chars[i] == '(' {
                left += 1;
            } else {
                right += 1;
            }

            if right > left {
                left = 0;
                right = 0;
            }

            if left == right {
                max_len = max_len.max(left + right);
            }
        }

        // Right to left pass
        left = 0;
        right = 0;
        for i in (0..n).rev() {
            if chars[i] == '(' {
                left += 1;
            } else {
                right += 1;
            }

            if left > right {
                left = 0;
                right = 0;
            }

            if left == right {
                max_len = max_len.max(left + right);
            }
        }

        max_len as i32
    }
}
```