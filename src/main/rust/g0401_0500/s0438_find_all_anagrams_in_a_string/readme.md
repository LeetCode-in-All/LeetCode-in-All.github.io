[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 438\. Find All Anagrams in a String

Medium

Given two strings `s` and `p`, return _an array of all the start indices of_ `p`_'s anagrams in_ `s`. You may return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** s = "cbaebabacd", p = "abc"

**Output:** [0,6]

**Explanation:** 

The substring with start index = 0 is "cba", which is an anagram of "abc". 

The substring with start index = 6 is "bac", which is an anagram of "abc".

**Example 2:**

**Input:** s = "abab", p = "ab"

**Output:** [0,1,2]

**Explanation:** 

The substring with start index = 0 is "ab", which is an anagram of "ab". 

The substring with start index = 1 is "ba", which is an anagram of "ab". 

The substring with start index = 2 is "ab", which is an anagram of "ab".

**Constraints:**

*   <code>1 <= s.length, p.length <= 3 * 10<sup>4</sup></code>
*   `s` and `p` consist of lowercase English letters.

## Solution

```rust
use std::collections::VecDeque;

impl Solution {
    pub fn find_anagrams(s: String, p: String) -> Vec<i32> {
        let mut map = vec![0; 26];
        let p_len = p.len();
        let s_len = s.len();
        
        // Fill the map with the character frequencies of string `p`
        for ch in p.chars() {
            map[ch as usize - 'a' as usize] += 1;
        }

        let mut res = Vec::new();
        let mut j = 0;

        // Sliding window
        for i in 0..s_len {
            let idx = s.as_bytes()[i] as usize - 'a' as usize;
            map[idx] -= 1;

            // If window size exceeds p_len, remove the left character
            if i >= p_len {
                let left_idx = s.as_bytes()[j] as usize - 'a' as usize;
                map[left_idx] += 1;
                j += 1;
            }

            // Check if the window is an anagram of `p`
            if i >= p_len - 1 && map.iter().all(|&x| x == 0) {
                res.push(j as i32);
            }
        }

        res
    }
}
```