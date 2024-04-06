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

```ruby
# @param {String} word1
# @param {String} word2
# @return {Integer}
def min_distance(word1, word2)
  n1 = word1.length
  n2 = word2.length

  return min_distance(word2, word1) if n2 > n1

  dp = Array.new(n2 + 1) {|j| j}

  (1..n1).each do |i|
    pre = dp[0]
    dp[0] = i

    (1..n2).each do |j|
      tmp = dp[j]
      dp[j] = word1[i - 1] != word2[j - 1] ? 1 + [pre, dp[j], dp[j - 1]].min : pre
      pre = tmp
    end
  end

  dp[n2]
end
```