[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 10\. Regular Expression Matching

Hard

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:

*   `'.'` Matches any single character.
*   `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

**Example 1:**

**Input:** s = "aa", p = "a"

**Output:** false

**Explanation:** "a" does not match the entire string "aa". 

**Example 2:**

**Input:** s = "aa", p = "a\*"

**Output:** true

**Explanation:** '\*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa". 

**Example 3:**

**Input:** s = "ab", p = ".\*"

**Output:** true

**Explanation:** ".\*" means "zero or more (\*) of any character (.)". 

**Example 4:**

**Input:** s = "aab", p = "c\*a\*b"

**Output:** true

**Explanation:** c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab". 

**Example 5:**

**Input:** s = "mississippi", p = "mis\*is\*p\*."

**Output:** false 

**Constraints:**

*   `1 <= s.length <= 20`
*   `1 <= p.length <= 30`
*   `s` contains only lowercase English letters.
*   `p` contains only lowercase English letters, `'.'`, and `'*'`.
*   It is guaranteed for each appearance of the character `'*'`, there will be a previous valid character to match.

## Solution

```csharp
public class Solution {
    private bool?[,] cache;

    public bool IsMatch(string s, string p) {
        cache = new bool?[s.Length + 1, p.Length + 1];
        return IsMatch(s, p, 0, 0);
    }

    private bool IsMatch(string s, string p, int i, int j) {
        if (j == p.Length) {
            return i == s.Length;
        }
        bool result;
        if (cache[i, j] != null) {
            return cache[i, j].Value;
        }
        bool firstMatch = i < s.Length && (s[i] == p[j] || p[j] == '.');
        if ((j + 1) < p.Length && p[j + 1] == '*') {
            result = (firstMatch && IsMatch(s, p, i + 1, j)) || IsMatch(s, p, i, j + 2);
        } else {
            result = firstMatch && IsMatch(s, p, i + 1, j + 1);
        }
        cache[i, j] = result;
        return result;
    }
}
```