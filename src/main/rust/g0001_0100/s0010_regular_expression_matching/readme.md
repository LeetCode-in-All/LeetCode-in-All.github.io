[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 10\. Regular Expression Matching

Hard

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:

*   `'.'` Matches any single character.
*   `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

**Example 1:**

**Input:** s = "aa", p = "a"

**Output:** false

**Explanation:** "a" does not match the entire string "aa". 

**Example 2:**

**Input:** s = "aa", p = "a\*"

**Output:** true

**Explanation:** '\*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa". 

**Example 3:**

**Input:** s = "ab", p = ".\*"

**Output:** true

**Explanation:** ".\*" means "zero or more (\*) of any character (.)". 

**Example 4:**

**Input:** s = "aab", p = "c\*a\*b"

**Output:** true

**Explanation:** c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab". 

**Example 5:**

**Input:** s = "mississippi", p = "mis\*is\*p\*."

**Output:** false 

**Constraints:**

*   `1 <= s.length <= 20`
*   `1 <= p.length <= 30`
*   `s` contains only lowercase English letters.
*   `p` contains only lowercase English letters, `'.'`, and `'*'`.
*   It is guaranteed for each appearance of the character `'*'`, there will be a previous valid character to match.

## Solution

```rust
impl Solution {
    pub fn is_match(s: String, p: String) -> bool {
        is_match_dp(s.as_bytes(), p.as_bytes())
    }
}

pub fn is_match_dp(s: &[u8], p: &[u8]) -> bool {
    let mut grid = vec![vec![false; s.len() + 1]; p.len() + 1];
    grid[p.len()][s.len()] = true;

    let mut pi = p.len();
    while pi > 0 {
        pi -= 1;

        let mstar = pi > 0 && p[pi] == b'*';
        if mstar {
            pi -= 1;
        }

        for si in 0..=s.len() {
            let is_match = if mstar {
                let mut si2 = si;
                loop {
                    if grid[pi + 2][si2] {
                        break true;
                    }
                    if si2 < s.len() && (p[pi] == b'.' || s[si2] == p[pi]) {
                        si2 += 1;
                        continue;
                    }
                    break false;
                }
            } else {
                si < s.len() && (p[pi] == b'.' || s[si] == p[pi]) && grid[pi + 1][si + 1]
            };
            grid[pi][si] = is_match;
        }
    }

    grid[0][0]
}
```