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

To solve this task, we can use a backtracking approach. 

## Solution

```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        res = []
        self.backtracking(res, [], s, 0)
        return res

    def backtracking(self, res, curr_arr, s, start):
        if start == len(s):
            res.append(list(curr_arr))
            return
        for end in range(start, len(s)):
            if not self.is_palindrome(s, start, end):
                continue
            curr_arr.append(s[start:end + 1])
            self.backtracking(res, curr_arr, s, end + 1)
            curr_arr.pop()

    def is_palindrome(self, s, start, end):
        while start < end and s[start] == s[end]:
            start += 1
            end -= 1
        return start >= end
```