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

```csharp
public class Solution {
    public IList<IList<string>> Partition(string s) {
        IList<IList<string>> res = new List<IList<string>>();
        Backtracking(res, new List<string>(), s, 0);
        return res;
    }

    private void Backtracking(IList<IList<string>> res, IList<string> currArr, string s, int start) {
        if (start == s.Length) {
            res.Add(new List<string>(currArr));
        }
        for (int end = start; end < s.Length; end++) {
            if (!IsPanlindrome(s, start, end)) {
                continue;
            }
            currArr.Add(s.Substring(start, end - start + 1));
            Backtracking(res, currArr, s, end + 1);
            currArr.RemoveAt(currArr.Count - 1);
        }
    }

    private bool IsPanlindrome(string s, int start, int end) {
        while (start < end && s[start] == s[end]) {
            start++;
            end--;
        }
        return start >= end;
    }
}
```