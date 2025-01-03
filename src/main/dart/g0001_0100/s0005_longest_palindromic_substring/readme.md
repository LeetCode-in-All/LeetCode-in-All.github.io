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

```dart
class Solution {
  String longestPalindrome(String s) {
    List<String> newStr = List.filled(s.length * 2 + 1, '#');

    for (int i = 0; i < s.length; i++) {
      newStr[2 * i + 1] = s[i];
      newStr[2 * i + 2] = '#';
    }

    List<int> dp = List.filled(newStr.length, 0);
    int friendCenter = 0;
    int friendRadius = 0;
    int lpsCenter = 0;
    int lpsRadius = 0;

    for (int i = 0; i < newStr.length; i++) {
      dp[i] = (friendCenter + friendRadius > i)
          ? (dp[friendCenter * 2 - i] < (friendCenter + friendRadius) - i
          ? dp[friendCenter * 2 - i]
          : (friendCenter + friendRadius) - i)
          : 1;

      while (i + dp[i] < newStr.length &&
          i - dp[i] >= 0 &&
          newStr[i + dp[i]] == newStr[i - dp[i]]) {
        dp[i]++;
      }

      if (friendCenter + friendRadius < i + dp[i]) {
        friendCenter = i;
        friendRadius = dp[i];
      }

      if (lpsRadius < dp[i]) {
        lpsCenter = i;
        lpsRadius = dp[i];
      }
    }

    return s.substring(
        (lpsCenter - lpsRadius + 1) ~/ 2, (lpsCenter + lpsRadius - 1) ~/ 2);
  }
}
```