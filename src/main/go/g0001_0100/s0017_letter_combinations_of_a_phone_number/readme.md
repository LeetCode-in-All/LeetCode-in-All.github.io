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

```golang
func letterCombinations(digits string) []string {
	if len(digits) == 0 {
		return nil
	}
	letters := []string{"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"}
	var ans []string
	var sb string
	findCombinations(0, digits, letters, &sb, &ans)
	return ans
}

func findCombinations(start int, nums string, letters []string, curr *string, ans *[]string) {
	if len(*curr) == len(nums) {
		*ans = append(*ans, *curr)
		return
	}
	for i := start; i < len(nums); i++ {
		n := int(nums[i] - '0')
		for j := 0; j < len(letters[n]); j++ {
			ch := letters[n][j]
			*curr += string(ch)
			findCombinations(i+1, nums, letters, curr, ans)
			*curr = (*curr)[:len(*curr)-1]
		}
	}
}
```