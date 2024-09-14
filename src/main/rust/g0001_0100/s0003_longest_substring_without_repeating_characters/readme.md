[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 3\. Longest Substring Without Repeating Characters

Medium

Given a string `s`, find the length of the **longest substring** without repeating characters.

**Example 1:**

**Input:** s = "abcabcbb"

**Output:** 3

**Explanation:** The answer is "abc", with the length of 3. 

**Example 2:**

**Input:** s = "bbbbb"

**Output:** 1

**Explanation:** The answer is "b", with the length of 1. 

**Example 3:**

**Input:** s = "pwwkew"

**Output:** 3

**Explanation:** The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring. 

**Example 4:**

**Input:** s = ""

**Output:** 0 

**Constraints:**

*   <code>0 <= s.length <= 5 * 10<sup>4</sup></code>
*   `s` consists of English letters, digits, symbols and spaces.

## Solution

```rust
impl Solution {
    pub fn length_of_longest_substring(s: String) -> i32 {
        // Array to store last seen indices of characters
        let mut last_indices = [-1; 256];
        let mut max_len = 0;
        let mut cur_len = 0;
        let mut start = 0;

        // Convert string to bytes to use indexing
        let bytes = s.as_bytes();
        for (i, &cur) in bytes.iter().enumerate() {
            // Cast byte to usize to use as an index
            let cur = cur as usize;

            if last_indices[cur] < start as i32 {
                last_indices[cur] = i as i32;
                cur_len += 1;
            } else {
                let last_index = last_indices[cur];
                start = (last_index + 1) as usize;
                cur_len = i - start + 1;
                last_indices[cur] = i as i32;
            }

            if cur_len > max_len {
                max_len = cur_len;
            }
        }

        max_len as i32
    }
}
```