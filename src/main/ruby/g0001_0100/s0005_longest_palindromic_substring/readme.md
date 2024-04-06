[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 5\. Longest Palindromic Substring

Medium

Given a string `s`, return _the longest palindromic substring_ in `s`.

**Example 1:**

**Input:** s = "babad"

**Output:** "bab" **Note:** "aba" is also a valid answer. 

**Example 2:**

**Input:** s = "cbbd"

**Output:** "bb" 

**Example 3:**

**Input:** s = "a"

**Output:** "a" 

**Example 4:**

**Input:** s = "ac"

**Output:** "a" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consist of only digits and English letters.

## Solution

```ruby
# @param {String} s
# @return {String}
def longest_palindrome(s)
  new_str = Array.new(s.length * 2 + 1, 0)
  new_str[0] = '#'

  (0...s.length).each do |i|
    new_str[2 * i + 1] = s[i]
    new_str[2 * i + 2] = '#'
  end

  dp = Array.new(new_str.length, 0)
  friend_center = 0
  friend_radius = 0
  lps_center = 0
  lps_radius = 0

  (0...new_str.length).each do |i|
    dp[i] = friend_center + friend_radius > i ? [dp[2 * friend_center - i], friend_center + friend_radius - i].min : 1

    while i + dp[i] < new_str.length && i - dp[i] >= 0 && new_str[i + dp[i]] == new_str[i - dp[i]]
      dp[i] += 1
    end

    if friend_center + friend_radius < i + dp[i]
      friend_center = i
      friend_radius = dp[i]
    end

    lps_center, lps_radius = i, dp[i] if lps_radius < dp[i]
  end

  s[(lps_center - lps_radius + 1) / 2, lps_radius - 1]
end
```