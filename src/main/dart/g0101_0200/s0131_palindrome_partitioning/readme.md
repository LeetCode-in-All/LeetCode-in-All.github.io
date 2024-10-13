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

```dart
class Solution {
  List<List<String>> partition(String s) {
    // Time Complexity: O(n * 2^n)
    // Space Complexity: O(n^2)

    List<List<String>> result = [];
    List<String> path = [];

    bool isPalindrome(String s) {
      int left = 0, right = s.length - 1;
      while (left < right) {
        if (s[left] != s[right]) return false;
        left++;
        right--;
      }
      return true;
    }

    void backtrack(int start) {
      if (start == s.length) {
        result.add(List.from(path));
        return;
      }
      for (int end = start + 1; end <= s.length; end++) {
        String substr = s.substring(start, end);
        if (isPalindrome(substr)) {
          path.add(substr);
          backtrack(end);
          path.removeLast();
        }
      }
    }

    backtrack(0);
    return result;
  }
}
```