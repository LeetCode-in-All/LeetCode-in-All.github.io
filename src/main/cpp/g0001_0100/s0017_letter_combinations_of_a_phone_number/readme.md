[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 17\. Letter Combinations of a Phone Number

Medium

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**Example 1:**

**Input:** digits = "23"

**Output:** ["ad","ae","af","bd","be","bf","cd","ce","cf"] 

**Example 2:**

**Input:** digits = ""

**Output:** [] 

**Example 3:**

**Input:** digits = "2"

**Output:** ["a","b","c"] 

**Constraints:**

*   `0 <= digits.length <= 4`
*   `digits[i]` is a digit in the range `['2', '9']`.



## Solution

```cpp
#include <vector>
#include <string>
#include <unordered_map>
using namespace std;

class Solution {
public:
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) {
            return {};
        }

        vector<string> letters = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        vector<string> ans;
        string curr;
        findCombinations(0, digits, letters, curr, ans);
        return ans;
    }

private:
    void findCombinations(int start, const string& nums, const vector<string>& letters, string& curr, vector<string>& ans) {
        if (curr.length() == nums.length()) {
            ans.push_back(curr);
            return;
        }

        int n = nums[start] - '0';
        for (char ch : letters[n]) {
            curr.push_back(ch);
            findCombinations(start + 1, nums, letters, curr, ans);
            curr.pop_back();
        }
    }
};
```