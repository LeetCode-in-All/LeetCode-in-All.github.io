[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 76\. Minimum Window Substring

Hard

Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window substring** of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window. If there is no such substring__, return the empty string_ `""`_._

The testcases will be generated such that the answer is **unique**.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "ADOBECODEBANC", t = "ABC"

**Output:** "BANC"

**Explanation:** The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t. 

**Example 2:**

**Input:** s = "a", t = "a"

**Output:** "a"

**Explanation:** The entire string s is the minimum window. 

**Example 3:**

**Input:** s = "a", t = "aa"

**Output:** ""

**Explanation:** Both 'a's from t must be included in the window. Since the largest window of s only has one 'a', return empty string. 

**Constraints:**

*   `m == s.length`
*   `n == t.length`
*   <code>1 <= m, n <= 10<sup>5</sup></code>
*   `s` and `t` consist of uppercase and lowercase English letters.

**Follow up:** Could you find an algorithm that runs in `O(m + n)` time?

## Solution

```ruby
# @param {String} s
# @param {String} t
# @return {String}
def min_window(s, t)
  return '' if t.size > s.size

  fixnum_max = (2 ** (0.size * 8 - 2) - 1)
  mp = Hash.new(0)
  t.each_char do |c|
    mp[c] += 1
  end

  begin_ptr = 0
  end_ptr = 0
  counter = mp.size
  len = fixnum_max
  head = 0

  while end_ptr < s.size
    ch = s[end_ptr].chr
    if mp.include?(ch)
      mp[ch] -= 1
      counter -= 1 if mp[ch].zero?
    end
    end_ptr += 1

    while counter.zero?
      tmp = s[begin_ptr].chr
      if mp.include?(tmp)
        mp[tmp] += 1
        counter += 1 if mp[tmp].positive?
      end

      if end_ptr - begin_ptr < len
        len = end_ptr - begin_ptr
        head = begin_ptr
      end
      begin_ptr += 1
    end
  end

  len == fixnum_max ? '' : s[head..head + len - 1]
end
```