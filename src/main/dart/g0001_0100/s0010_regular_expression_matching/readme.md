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

```dart
class Solution {
  List<List<bool?>>? cache;

  bool isMatch(String s, String p) {
    // Initialize the cache with null values, similar to Boolean[][] in Java
    cache = List.generate(s.length + 1, (_) => List.filled(p.length + 1, null));
    return isMatchHelper(s, p, 0, 0);
  }

  bool isMatchHelper(String s, String p, int i, int j) {
    // If pattern is fully traversed, check if string is fully matched
    if (j == p.length) {
      return i == s.length;
    }

    // Return cached result if available
    if (cache![i][j] != null) {
      return cache![i][j]!;
    }

    // Check if first characters match (either the same or the pattern has '.')
    bool firstMatch = i < s.length && (s[i] == p[j] || p[j] == '.');

    bool result;

    // Handle '*' wildcard in the pattern
    if (j + 1 < p.length && p[j + 1] == '*') {
      result = (firstMatch && isMatchHelper(s, p, i + 1, j)) ||
          isMatchHelper(s, p, i, j + 2);
    } else {
      result = firstMatch && isMatchHelper(s, p, i + 1, j + 1);
    }

    // Store the result in the cache
    cache![i][j] = result;
    return result;
  }
}
```