[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 139\. Word Break

Medium

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

**Input:** s = "leetcode", wordDict = ["leet","code"]

**Output:** true

**Explanation:** Return true because "leetcode" can be segmented as "leet code". 

**Example 2:**

**Input:** s = "applepenapple", wordDict = ["apple","pen"]

**Output:** true

**Explanation:** Return true because "applepenapple" can be segmented as "apple pen apple". Note that you are allowed to reuse a dictionary word. 

**Example 3:**

**Input:** s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]

**Output:** false 

**Constraints:**

*   `1 <= s.length <= 300`
*   `1 <= wordDict.length <= 1000`
*   `1 <= wordDict[i].length <= 20`
*   `s` and `wordDict[i]` consist of only lowercase English letters.
*   All the strings of `wordDict` are **unique**.

## Solution

```php
class Solution {
    /**
     * @param String $s
     * @param String[] $wordDict
     * @return Boolean
     */
    public function wordBreak($s, $wordDict) {
        $set = array();
        $max = 0;
        $flag = array_fill(0, strlen($s) + 1, false);
        foreach ($wordDict as $st) {
            $set[$st] = true;
            if ($max < strlen($st)) {
                $max = strlen($st);
            }
        }
        for ($i = 1; $i <= $max; $i++) {
            if ($this->dfs($s, 0, $i, $max, $set, $flag)) {
                return true;
            }
        }
        return false;
    }

    private function dfs($s, $start, $end, $max, $set, &$flag) {
        if (!$flag[$end] && isset($set[substr($s, $start, $end - $start)])) {
            $flag[$end] = true;
            if ($end == strlen($s)) {
                return true;
            }
            for ($i = 1; $i <= $max; $i++) {
                if ($end + $i <= strlen($s) && $this->dfs($s, $end, $end + $i, $max, $set, $flag)) {
                    return true;
                }
            }
        }
        return false;
    }
}
```