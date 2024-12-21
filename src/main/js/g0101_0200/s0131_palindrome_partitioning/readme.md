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

```javascript
/**
 * @param {string} s
 * @return {string[][]}
 */
var partition = function(s) {
    const res = []
    backtracking(res, [], s, 0)
    return res
};

const backtracking = (res, currArr, s, start) => {
    if (start === s.length) {
        res.push([...currArr]) // Add a copy of the current array to the result
        return
    }

    for (let end = start; end < s.length; end++) {
        if (!isPalindrome(s, start, end)) {
            continue
        }
        currArr.push(s.substring(start, end + 1)) // Add the current substring
        backtracking(res, currArr, s, end + 1) // Recurse to the next part
        currArr.pop() // Remove the last element to backtrack
    }
};

const isPalindrome = (s, start, end) => {
    while (start < end && s[start] === s[end]) {
        start++
        end--
    }
    return start >= end
};

export { partition }
```