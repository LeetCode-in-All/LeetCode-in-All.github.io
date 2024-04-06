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

```ruby
# @param {String} s
# @return {Integer}
def longest_valid_parentheses(s)
  max = 0
  left = 0
  right = 0
  n = s.length
  ch = nil

  (0...n).each do |i|
    ch = s[i]
    if ch == '('
      left += 1
    else
      right += 1
    end

    if right > left
      left = 0
      right = 0
    end

    if left == right
      max = [max, left + right].max
    end
  end

  left = 0
  right = 0

  (n - 1).downto(0) do |i|
    ch = s[i]
    if ch == '('
      left += 1
    else
      right += 1
    end

    if left > right
      left = 0
      right = 0
    end

    if left == right
      max = [max, left + right].max
    end
  end

  max
end
```