[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 647\. Palindromic Substrings

Medium

Given a string `s`, return _the number of **palindromic substrings** in it_.

A string is a **palindrome** when it reads the same backward as forward.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "abc"

**Output:** 3

**Explanation:** Three palindromic strings: "a", "b", "c".

**Example 2:**

**Input:** s = "aaa"

**Output:** 6

**Explanation:** Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consists of lowercase English letters.

## Solution

```rust
impl Solution {
    fn expand(s: &[char], mut l: i32, mut r: i32, res: &mut i32) {
        while l >= 0 && (r as usize) < s.len() {
            if s[l as usize] != s[r as usize] {
                return;
            } else {
                *res += 1;
                l -= 1;
                r += 1;
            }
        }
    }

    pub fn count_substrings(s: String) -> i32 {
        let a: Vec<char> = s.chars().collect();
        let mut res = 0;
        for i in 0..a.len() {
            Solution::expand(&a, i as i32, i as i32, &mut res);       // Odd length palindromes
            Solution::expand(&a, i as i32, (i + 1) as i32, &mut res); // Even length palindromes
        }
        res
    }
}
```