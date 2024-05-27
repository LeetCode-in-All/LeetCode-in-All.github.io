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

```ruby
# @param {String} s
# @return {Integer}
def length_of_longest_substring(s)
  last_indices = Array.new(256, -1)
  max_len = 0
  cur_len = 0
  start = 0

  s.each_char.with_index do |cur, i|
    cur = cur.ord
    if last_indices[cur] < start
      last_indices[cur] = i
      cur_len += 1
    else
      last_index = last_indices[cur]
      start = last_index + 1
      cur_len = i - start + 1
      last_indices[cur] = i
    end

    max_len = cur_len if cur_len > max_len
  end

  max_len
end
```