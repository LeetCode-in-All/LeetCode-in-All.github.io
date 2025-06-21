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

```csharp
using System.Text;

public class Solution {
    public IList<string> LetterCombinations(string digits) {
        if (string.IsNullOrEmpty(digits)) {
            return new List<string>();
        }
        string[] letters = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        List<string> ans = new List<string>();
        StringBuilder sb = new StringBuilder();
        FindCombinations(0, digits, letters, sb, ans);
        return ans;
    }

    private void FindCombinations(
            int start, string nums, string[] letters, StringBuilder curr, List<string> ans) {
        if (curr.Length == nums.Length) {
            ans.Add(curr.ToString());
            return;
        }
        for (int i = start; i < nums.Length; i++) {
            int n = nums[i] - '0'; // Convert char to int
            for (int j = 0; j < letters[n].Length; j++) {
                char ch = letters[n][j];
                curr.Append(ch);
                FindCombinations(i + 1, nums, letters, curr, ans);
                curr.Remove(curr.Length - 1, 1); // Remove last character
            }
        }
    }
}
```