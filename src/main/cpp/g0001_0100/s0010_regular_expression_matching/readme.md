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

```cpp
#include <vector>
#include <string>

class Solution {
public:
    std::vector<std::vector<std::optional<bool>>> cache;

    bool isMatch(const std::string& s, const std::string& p) {
        cache.resize(s.length() + 1, std::vector<std::optional<bool>>(p.length() + 1));
        return isMatchHelper(s, p, 0, 0);
    }

private:
    bool isMatchHelper(const std::string& s, const std::string& p, int i, int j) {
        if (j == p.length()) {
            return i == s.length();
        }

        if (cache[i][j].has_value()) {
            return cache[i][j].value();
        }

        bool firstMatch = (i < s.length() && (s[i] == p[j] || p[j] == '.'));

        bool result;
        if ((j + 1) < p.length() && p[j + 1] == '*') {
            result = (firstMatch && isMatchHelper(s, p, i + 1, j)) || isMatchHelper(s, p, i, j + 2);
        } else {
            result = firstMatch && isMatchHelper(s, p, i + 1, j + 1);
        }

        cache[i][j] = result;
        return result;
    }
};
```