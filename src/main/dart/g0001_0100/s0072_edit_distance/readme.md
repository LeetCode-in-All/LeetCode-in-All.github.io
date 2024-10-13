[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 72\. Edit Distance

Hard

Given two strings `word1` and `word2`, return _the minimum number of operations required to convert `word1` to `word2`_.

You have the following three operations permitted on a word:

*   Insert a character
*   Delete a character
*   Replace a character

**Example 1:**

**Input:** word1 = "horse", word2 = "ros"

**Output:** 3

**Explanation:** 

horse -> rorse (replace 'h' with 'r') 

rorse -> rose (remove 'r') 

rose -> ros (remove 'e')

**Example 2:**

**Input:** word1 = "intention", word2 = "execution"

**Output:** 5

**Explanation:** 

intention -> inention (remove 't') 

inention -> enention (replace 'i' with 'e') 

enention -> exention (replace 'n' with 'x') 

exention -> exection (replace 'n' with 'c') 

exection -> execution (insert 'u')

**Constraints:**

*   `0 <= word1.length, word2.length <= 500`
*   `word1` and `word2` consist of lowercase English letters.

## Solution

```dart
class Solution {
  int minDistance(String w1, String w2) {
    int n1 = w1.length;
    int n2 = w2.length;

    // If w2 is longer, swap w1 and w2 to ensure w1 is the longer string
    if (n2 > n1) {
      return minDistance(w2, w1);
    }

    List<int> dp = List.filled(n2 + 1, 0);

    // Initialize the first row of the DP table
    for (int j = 0; j <= n2; j++) {
      dp[j] = j;
    }

    for (int i = 1; i <= n1; i++) {
      int pre = dp[0];
      dp[0] = i;
      for (int j = 1; j <= n2; j++) {
        int temp = dp[j];
        dp[j] = w1[i - 1] != w2[j - 1]
            ? 1 + [pre, dp[j], dp[j - 1]].reduce((a, b) => a < b ? a : b)
            : pre;
        pre = temp;
      }
    }

    return dp[n2];
  }
}
```