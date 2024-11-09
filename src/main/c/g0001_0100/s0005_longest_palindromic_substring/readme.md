[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 5\. Longest Palindromic Substring

Medium

Given a string `s`, return _the longest palindromic substring_ in `s`.

**Example 1:**

**Input:** s = "babad"

**Output:** "bab" **Note:** "aba" is also a valid answer. 

**Example 2:**

**Input:** s = "cbbd"

**Output:** "bb" 

**Example 3:**

**Input:** s = "a"

**Output:** "a" 

**Example 4:**

**Input:** s = "ac"

**Output:** "a" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consist of only digits and English letters.

## Solution

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char* longestPalindrome(const char* s) {
    int len = strlen(s);
    
    // Create new string with inserted '#' characters
    int newLen = len * 2 + 1;
    char* newStr = (char*)malloc(newLen + 1);
    newStr[0] = '#';
    for (int i = 0; i < len; i++) {
        newStr[2 * i + 1] = s[i];
        newStr[2 * i + 2] = '#';
    }
    newStr[newLen] = '\0';
    
    int* dp = (int*)malloc(newLen * sizeof(int));
    int friendCenter = 0;
    int friendRadius = 0;
    int lpsCenter = 0;
    int lpsRadius = 0;

    for (int i = 0; i < newLen; i++) {
        dp[i] = (friendCenter + friendRadius > i) ? 
                 (dp[2 * friendCenter - i] < (friendCenter + friendRadius - i) ? dp[2 * friendCenter - i] : (friendCenter + friendRadius - i)) 
                 : 1;
        
        // Expanding around center
        while (i + dp[i] < newLen && i - dp[i] >= 0 && newStr[i + dp[i]] == newStr[i - dp[i]]) {
            dp[i]++;
        }

        // Update the friendCenter and friendRadius
        if (i + dp[i] > friendCenter + friendRadius) {
            friendCenter = i;
            friendRadius = dp[i];
        }

        // Update the longest palindromic substring center and radius
        if (dp[i] > lpsRadius) {
            lpsCenter = i;
            lpsRadius = dp[i];
        }
    }

    // Extract the original longest palindrome substring from 's'
    int start = (lpsCenter - lpsRadius + 1) / 2;
    int length = lpsRadius - 1;

    char* result = (char*)malloc(length + 1);
    strncpy(result, s + start, length);
    result[length] = '\0';

    // Free allocated memory
    free(newStr);
    free(dp);

    return result;
}
```