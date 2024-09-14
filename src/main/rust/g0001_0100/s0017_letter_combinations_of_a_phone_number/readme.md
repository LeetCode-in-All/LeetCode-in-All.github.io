[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 17\. Letter Combinations of a Phone Number

Medium

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**Example 1:**

**Input:** digits = "23"

**Output:** ["ad","ae","af","bd","be","bf","cd","ce","cf"]

**Example 2:**

**Input:** digits = ""

**Output:** []

**Example 3:**

**Input:** digits = "2"

**Output:** ["a","b","c"]

**Constraints:**

*   `0 <= digits.length <= 4`
*   `digits[i]` is a digit in the range `['2', '9']`.

## Solution

```rust
impl Solution {
    pub fn letter_combinations(digits: String) -> Vec<String> {
        if digits.is_empty() {
            return vec![];
        }

        let letters = vec![
            "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"
        ];

        let mut ans = vec![];
        let mut sb = String::new();
        Solution::find_combinations(0, &digits, &letters, &mut sb, &mut ans);
        ans
    }

    fn find_combinations(
        start: usize,
        digits: &str,
        letters: &[&str],
        curr: &mut String,
        ans: &mut Vec<String>,
    ) {
        if curr.len() == digits.len() {
            ans.push(curr.clone());
            return;
        }

        for i in start..digits.len() {
            let n = digits.chars().nth(i).unwrap().to_digit(10).unwrap() as usize;
            for ch in letters[n].chars() {
                curr.push(ch);
                Solution::find_combinations(i + 1, digits, letters, curr, ans);
                curr.pop();
            }
        }
    }
}
```