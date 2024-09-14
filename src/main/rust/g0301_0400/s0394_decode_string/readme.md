[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 394\. Decode String

Medium

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed <code>10<sup>5</sup></code>.

**Example 1:**

**Input:** s = "3[a]2[bc]"

**Output:** "aaabcbc"

**Example 2:**

**Input:** s = "3[a2[c]]"

**Output:** "accaccacc"

**Example 3:**

**Input:** s = "2[abc]3[cd]ef"

**Output:** "abcabccdcdcdef"

**Constraints:**

*   `1 <= s.length <= 30`
*   `s` consists of lowercase English letters, digits, and square brackets `'[]'`.
*   `s` is guaranteed to be **a valid** input.
*   All the integers in `s` are in the range `[1, 300]`.

## Solution

```rust
impl Solution {
    pub fn decode_string(s: String) -> String {
        s
        .chars()
        .fold((String::new(), String::new(), Vec::new()), |(mut next_string, mut next_integer, mut stack): (String, String, Vec<(usize, String)>), c| {
            match c {
                '0'..='9' => {
                    next_integer.push(c);
                    (next_string, next_integer, stack)
                },
                '[' => {
                    stack.push((next_integer.parse::<usize>().unwrap(), next_string));
                    next_integer.clear();
                    (String::new(), next_integer, stack)
                },
                ']' => {
                    let (last_integer, left_string) = stack.pop().unwrap();
                    let next_string = left_string + &next_string.repeat(last_integer);
                    (next_string, next_integer, stack)
                },
                c => {
                    next_string.push(c);
                    (next_string, next_integer, stack)
                }
            }
        }).0
    }
}
```