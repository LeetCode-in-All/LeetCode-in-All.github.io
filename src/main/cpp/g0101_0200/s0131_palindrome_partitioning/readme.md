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

```cpp
#include <vector>
#include <string>

class Solution {
public:
    std::vector<std::vector<std::string>> partition(std::string s) {
        std::vector<std::vector<std::string>> res;
        std::vector<std::string> currArr;
        backtracking(res, currArr, s, 0);
        return res;
    }

private:
    void backtracking(std::vector<std::vector<std::string>>& res, std::vector<std::string>& currArr, const std::string& s, int start) {
        if (start == s.length()) {
            res.push_back(currArr);
        }
        for (int end = start; end < s.length(); end++) {
            if (!isPalindrome(s, start, end)) {
                continue;
            }
            currArr.push_back(s.substr(start, end - start + 1));
            backtracking(res, currArr, s, end + 1);
            currArr.pop_back();
        }
    }

    bool isPalindrome(const std::string& s, int start, int end) {
        while (start < end && s[start] == s[end]) {
            start++;
            end--;
        }
        return start >= end;
    }
};
```