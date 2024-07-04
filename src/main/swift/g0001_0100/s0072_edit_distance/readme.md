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

To solve the "Edit Distance" problem in Swift with the Solution class, follow these steps:

1. Define a method `minDistance` in the `Solution` class that takes two strings `word1` and `word2` as input and returns the minimum number of operations required to convert `word1` to `word2`.
2. Initialize a 2D array `dp` of size `(m+1) x (n+1)`, where `m` is the length of `word1` and `n` is the length of `word2`.
3. Set `dp[i][0] = i` for all `i` from `0` to `m`, as the minimum number of operations to convert a string of length `i` to an empty string is `i` deletions.
4. Set `dp[0][j] = j` for all `j` from `0` to `n`, as the minimum number of operations to convert an empty string to a string of length `j` is `j` insertions.
5. Iterate over the characters of `word1` and `word2`:
   - If `word1.charAt(i-1)` is equal to `word2.charAt(j-1)`, set `dp[i][j] = dp[i-1][j-1]`, as no operation is required to match these characters.
   - Otherwise, set `dp[i][j]` to the minimum of the following three options:
     - `dp[i-1][j] + 1`: Delete the character at position `i` from `word1`.
     - `dp[i][j-1] + 1`: Insert the character at position `j` from `word2` into `word1`.
     - `dp[i-1][j-1] + 1`: Replace the character at position `i` in `word1` with the character at position `j` in `word2`.
6. Return `dp[m][n]`, which represents the minimum number of operations required to convert `word1` to `word2`.

Here's the implementation of the `minDistance` method in Swift:

```swift
class Solution {
    func minDistance(_ word1: String, _ word2: String) -> Int {
        var n = word1.count
        var m = word2.count
        if word1 == word2 { return 0}
        if m == 0 && n == 0 { return 0 }
        if m == 1 || n == 1 { return 1}
        var word1 = Array(word1)
        var word2 = Array(word2)
        var dp: [[Int]] = Array(repeating:Array(repeating: 0, count:m+1), count:n+1)
        for i in 0...n {
            dp[i][0] = i
        }
        for j in 0...m {
            dp[0][j] = j
        }
        for i in 1...n {
            for j in 1...m {
                if word1[i-1] == word2[j-1] {
                     dp[i][j] = dp[i-1][j-1]
                } else {
                     dp[i][j] = min(min(dp[i-1][j-1], dp[i-1][j]), dp[i][j-1]) + 1
                }
            }
        }
        return dp[n][m]
    }
}
```

This implementation efficiently calculates the minimum edit distance between two strings using dynamic programming, with a time complexity of O(m * n) and a space complexity of O(m * n), where m is the length of `word1` and n is the length of `word2`.