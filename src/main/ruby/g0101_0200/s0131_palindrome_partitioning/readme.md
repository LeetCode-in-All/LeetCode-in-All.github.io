[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 131\. Palindrome Partitioning

Medium

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

**Example 1:**

**Input:** s = "aab"

**Output:** [["a","a","b"],["aa","b"]] 

**Example 2:**

**Input:** s = "a"

**Output:** [["a"]] 

**Constraints:**

*   `1 <= s.length <= 16`
*   `s` contains only lowercase English letters.

## Solution

```ruby
# @param {String} s
# @return {String[][]}
def partition(s)
  res = []
  backtracking(res, [], s, 0)
  res
end

private

def backtracking(res, curr_arr, s, start)
  if start == s.length
    res << curr_arr.dup
  end

  (start...s.length).each do |end_idx|
    next unless is_palindrome?(s, start, end_idx)

    curr_arr << s[start..end_idx]
    backtracking(res, curr_arr, s, end_idx + 1)
    curr_arr.pop
  end
end

def is_palindrome?(s, start, end_idx)
  while start < end_idx && s[start] == s[end_idx]
    start += 1
    end_idx -= 1
  end
  start >= end_idx
end
```