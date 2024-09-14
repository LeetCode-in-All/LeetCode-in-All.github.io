[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 139\. Word Break

Medium

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

**Input:** s = "leetcode", wordDict = ["leet","code"]

**Output:** true

**Explanation:** Return true because "leetcode" can be segmented as "leet code".

**Example 2:**

**Input:** s = "applepenapple", wordDict = ["apple","pen"]

**Output:** true

**Explanation:** Return true because "applepenapple" can be segmented as "apple pen apple". 

Note that you are allowed to reuse a dictionary word.

**Example 3:**

**Input:** s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]

**Output:** false

**Constraints:**

*   `1 <= s.length <= 300`
*   `1 <= wordDict.length <= 1000`
*   `1 <= wordDict[i].length <= 20`
*   `s` and `wordDict[i]` consist of only lowercase English letters.
*   All the strings of `wordDict` are **unique**.

## Solution

```rust
impl Solution {
    pub fn word_break(s: String, word_dict: Vec<String>) -> bool {
        let mut state = vec![None::<bool>; s.len() + 1];
        word_break_0(&s, &word_dict, &mut state)
    }
}

fn word_break_0(s: &str, word_dict: &Vec<String>, state: &mut Vec<Option<bool>>) -> bool {
    if s.is_empty() {
        return true;
    }

    if let Some(result) = state[s.len()] {
        return result;
    }

    let result = word_dict
        .iter()
        .filter_map(|word| s.strip_prefix(word))
        .any(|new_s| word_break_0(new_s, word_dict, state));

    state[s.len()] = Some(result);

    result
}
```