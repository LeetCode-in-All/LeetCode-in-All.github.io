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

```cpp
#include <string>
#include <vector>
#include <unordered_set>
using namespace std;

class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> set;
        int maxLen = 0;
        vector<bool> flag(s.length() + 1, false);

        for (const string& word : wordDict) {
            set.insert(word);
            maxLen = max(maxLen, (int)word.length());
        }

        for (int i = 1; i <= maxLen; ++i) {
            if (dfs(s, 0, i, maxLen, set, flag)) {
                return true;
            }
        }
        return false;
    }

private:
    bool dfs(const string& s, int start, int end, int maxLen, unordered_set<string>& set, vector<bool>& flag) {
        if (!flag[end] && set.count(s.substr(start, end - start))) {
            flag[end] = true;
            if (end == s.length()) {
                return true;
            }
            for (int i = 1; i <= maxLen; ++i) {
                if (end + i <= s.length() && dfs(s, end, end + i, maxLen, set, flag)) {
                    return true;
                }
            }
        }
        return false;
    }
};
```