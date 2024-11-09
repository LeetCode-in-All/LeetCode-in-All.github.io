[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 3\. Longest Substring Without Repeating Characters

Medium

Given a string `s`, find the length of the **longest substring** without repeating characters.

**Example 1:**

**Input:** s = "abcabcbb"

**Output:** 3

**Explanation:** The answer is "abc", with the length of 3. 

**Example 2:**

**Input:** s = "bbbbb"

**Output:** 1

**Explanation:** The answer is "b", with the length of 1. 

**Example 3:**

**Input:** s = "pwwkew"

**Output:** 3

**Explanation:** The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring. 

**Example 4:**

**Input:** s = ""

**Output:** 0 

**Constraints:**

*   <code>0 <= s.length <= 5 * 10<sup>4</sup></code>
*   `s` consists of English letters, digits, symbols and spaces.

## Solution

```c
#include <stdio.h>
#include <string.h>

int lengthOfLongestSubstring(const char* s) {
    int lastIndices[256];
    for (int i = 0; i < 256; i++) {
        lastIndices[i] = -1;
    }

    int maxLen = 0;
    int curLen = 0;
    int start = 0;

    for (int i = 0; i < strlen(s); i++) {
        char cur = s[i];
        if (lastIndices[(unsigned char)cur] < start) {
            lastIndices[(unsigned char)cur] = i;
            curLen++;
        } else {
            int lastIndex = lastIndices[(unsigned char)cur];
            start = lastIndex + 1;
            curLen = i - start + 1;
            lastIndices[(unsigned char)cur] = i;
        }

        if (curLen > maxLen) {
            maxLen = curLen;
        }
    }

    return maxLen;
}
```