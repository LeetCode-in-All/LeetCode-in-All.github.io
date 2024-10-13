[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 22\. Generate Parentheses

Medium

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3

**Output:** ["((()))","(()())","(())()","()(())","()()()"]

**Example 2:**

**Input:** n = 1

**Output:** ["()"]

**Constraints:**

*   `1 <= n <= 8`

## Solution

```dart
class Solution {
  List<String> generateParenthesis(int n) {
    return parenthesis(n, n);
  }

  List<String> parenthesis(int left, int right) {
    if (left == 0 && right == 0) {
      return [""];
    }
    List<String> return_ls = [];
    if (left != 0) {
      List<String> l1 = parenthesis(left - 1, right);
      for (int i = 0; i < l1.length; ++i) {
        l1[i] = '(' + l1[i];
        return_ls.add(l1[i]);
      }
    }
    if (right != 0 && left < right) {
      List<String> r1 = parenthesis(left, right - 1);
      for (int i = 0; i < r1.length; ++i) {
        r1[i] = ')' + r1[i];
        return_ls.add(r1[i]);
      }
    }
    return return_ls;
  }
}
```