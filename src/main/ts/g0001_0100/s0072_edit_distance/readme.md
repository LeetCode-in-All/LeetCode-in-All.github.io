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

```typescript
function minDistance(word1: string, word2: string): number {
    const memo: number[][] = new Array(word1.length + 1).fill(0).map((_) => [])
    const l1 = word1.length
    const l2 = word2.length
    const dfs = (w1: number, w2: number): number => {
        if (memo[w1][w2] != undefined) return memo[w1][w2]
        if (w1 == l1 && w2 == l2) {
            memo[w1][w2] = 0
            return 0
        }
        if (w1 == l1 || w2 == l2) {
            memo[w1][w2] = Math.max(l1 - w1, l2 - w2)
            return memo[w1][w2]
        }
        let result = 0
        if (word1[w1] == word2[w2]) {
            result = dfs(w1 + 1, w2 + 1)
        } else {
            result = 1 + Math.min(dfs(w1 + 1, w2), dfs(w1 + 1, w2 + 1), dfs(w1, w2 + 1))
        }
        memo[w1][w2] = result
        return result
    }
    return dfs(0, 0)
}

export { minDistance }
```