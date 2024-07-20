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

**Explanation:** horse -> rorse (replace 'h' with 'r') rorse -> rose (remove 'r') rose -> ros (remove 'e') 

**Example 2:**

**Input:** word1 = "intention", word2 = "execution"

**Output:** 5

**Explanation:** intention -> inention (remove 't') inention -> enention (replace 'i' with 'e') enention -> exention (replace 'n' with 'x') exention -> exection (replace 'n' with 'c') exection -> execution (insert 'u') 

**Constraints:**

*   `0 <= word1.length, word2.length <= 500`
*   `word1` and `word2` consist of lowercase English letters.

## Solution

```csharp
public class Solution {
    public int MinDistance(string word1, string word2) {
        var map = new int[word1.Length + 1, word2.Length + 1];
        for (int i = 0; i <= word1.Length; i++) {
            map[i, 0] = i;
        }
        for (int i = 0; i <= word2.Length; i++) {
            map[0, i] = i;
        }
        for (int i = 1; i <= word1.Length; i++) {
            for (var j = 1; j <= word2.Length; j++) {
                var add = word1[i - 1] == word2[j - 1] ? 0 : 1;
                var min = Math.Min(map[i - 1, j] + 1, map[i, j - 1] + 1);
                map[i, j] = Math.Min(min, map[i - 1, j - 1] + add);
            }
        }
        return map[word1.Length, word2.Length];
    }
}
```