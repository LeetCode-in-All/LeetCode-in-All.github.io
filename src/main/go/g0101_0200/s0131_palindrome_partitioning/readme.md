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

```golang
func partition(s string) [][]string {
	var res [][]string
	backtracking(&res, []string{}, s, 0)
	return res
}

func backtracking(res *[][]string, currArr []string, s string, start int) {
	if start == len(s) {
		*res = append(*res, append([]string(nil), currArr...))
		return
	}
	for end := start; end < len(s); end++ {
		if !isPalindrome(s, start, end) {
			continue
		}
		currArr = append(currArr, s[start:end+1])
		backtracking(res, currArr, s, end+1)
		currArr = currArr[:len(currArr)-1]
	}
}

func isPalindrome(s string, start, end int) bool {
	for start < end {
		if s[start] != s[end] {
			return false
		}
		start++
		end--
	}
	return true
}
```