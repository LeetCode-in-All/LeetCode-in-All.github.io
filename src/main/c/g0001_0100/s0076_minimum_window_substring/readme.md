[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 76\. Minimum Window Substring

Hard

Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window substring** of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window. If there is no such substring__, return the empty string_ `""`_._

The testcases will be generated such that the answer is **unique**.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "ADOBECODEBANC", t = "ABC"

**Output:** "BANC"

**Explanation:** The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

**Example 2:**

**Input:** s = "a", t = "a"

**Output:** "a"

**Explanation:** The entire string s is the minimum window.

**Example 3:**

**Input:** s = "a", t = "aa"

**Output:** ""

**Explanation:** Both 'a's from t must be included in the window. Since the largest window of s only has one 'a', return empty string.

**Constraints:**

*   `m == s.length`
*   `n == t.length`
*   <code>1 <= m, n <= 10<sup>5</sup></code>
*   `s` and `t` consist of uppercase and lowercase English letters.

**Follow up:** Could you find an algorithm that runs in `O(m + n)` time?

## Solution

```c
#include <stdio.h>
#include <string.h>
#include <limits.h>

// Function to find the minimum window substring
char* minWindow(char* s, char* t) {
    // Lengths of strings s and t
    int sLen = strlen(s);
    int tLen = strlen(t);
    
    // Edge case: if either string is empty, return an empty string
    if (sLen == 0 || tLen == 0) {
        return "";
    }
    
    // Arrays to store character frequencies
    int need[256] = {0};  // To store required characters from t
    int window[256] = {0};  // To store characters in the current window of s
    
    // Initialize need array with frequencies of characters in t
    for (int i = 0; i < tLen; ++i) {
        need[t[i]]++;
    }
    
    int left = 0, right = 0;  // Pointers to define the current window in s
    int formed = 0;  // Count of how many required characters are satisfied in the current window
    int requiredChars = 0;  // Count of unique characters in t that need to be satisfied
    
    // Counting unique characters in t
    for (int i = 0; i < 256; ++i) {
        if (need[i] > 0) {
            requiredChars++;
        }
    }
    
    int minLen = sLen + 1;  // Initialize to a large value for minimum window length
    int minLeft = 0, minRight = 0;  // Indices to track the minimum window
    
    // Main loop to find the minimum window substring
    while (right < sLen) {
        char current = s[right];
        window[current]++;
        
        // If the current character is in t and its count matches the required count
        if (need[current] > 0 && window[current] == need[current]) {
            formed++;
        }
        
        // Try to shrink the window from the left
        while (formed == requiredChars && left <= right) {
            int currentLen = right - left + 1;
            
            // Update minimum length and indices if current window is smaller
            if (currentLen < minLen) {
                minLen = currentLen;
                minLeft = left;
                minRight = right;
            }
            
            char leftChar = s[left];
            window[leftChar]--;
            
            // If leftChar is in t and its count becomes less than required
            if (need[leftChar] > 0 && window[leftChar] < need[leftChar]) {
                formed--;
            }
            
            left++;  // Move left pointer to the right to shrink the window
        }
        
        right++;  // Move right pointer to the right to expand the window
    }
    
    // Check if a valid window was found
    if (minLen == sLen + 1) {
        return "";  // If no valid window found, return empty string
    } else {
        // Allocate memory for the result substring
        char* result = (char*)malloc((minLen + 1) * sizeof(char));
        strncpy(result, s + minLeft, minLen);
        result[minLen] = '\0';  // Null-terminate the string
        return result;
    }
}
```