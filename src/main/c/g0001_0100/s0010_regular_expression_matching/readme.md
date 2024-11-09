[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 10\. Regular Expression Matching

Hard

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:

*   `'.'` Matches any single character.
*   `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

**Example 1:**

**Input:** s = "aa", p = "a"

**Output:** false

**Explanation:** "a" does not match the entire string "aa". 

**Example 2:**

**Input:** s = "aa", p = "a\*"

**Output:** true

**Explanation:** '\*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa". 

**Example 3:**

**Input:** s = "ab", p = ".\*"

**Output:** true

**Explanation:** ".\*" means "zero or more (\*) of any character (.)". 

**Example 4:**

**Input:** s = "aab", p = "c\*a\*b"

**Output:** true

**Explanation:** c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab". 

**Example 5:**

**Input:** s = "mississippi", p = "mis\*is\*p\*."

**Output:** false 

**Constraints:**

*   `1 <= s.length <= 20`
*   `1 <= p.length <= 30`
*   `s` contains only lowercase English letters.
*   `p` contains only lowercase English letters, `'.'`, and `'*'`.
*   It is guaranteed for each appearance of the character `'*'`, there will be a previous valid character to match.

## Solution

```c
#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>
#include <string.h>

int** cache; // 2D array for caching results

// Helper function to initialize the cache with -1 values (indicating unvisited)
void initializeCache(int sLen, int pLen) {
    cache = (int**)malloc((sLen + 1) * sizeof(int*));
    for (int i = 0; i <= sLen; i++) {
        cache[i] = (int*)malloc((pLen + 1) * sizeof(int));
        for (int j = 0; j <= pLen; j++) {
            cache[i][j] = -1; // -1 indicates an unvisited state
        }
    }
}

// Recursive function to check for matches with caching
bool isMatchHelper(const char* s, const char* p, int i, int j) {
    int sLen = strlen(s);
    int pLen = strlen(p);

    // If pattern is exhausted, check if string is also exhausted
    if (j == pLen) {
        return i == sLen;
    }

    // Check cache to avoid recomputation
    if (cache[i][j] != -1) {
        return cache[i][j];
    }

    // Check if the current characters match
    bool firstMatch = (i < sLen && (s[i] == p[j] || p[j] == '.'));

    bool result;
    if ((j + 1) < pLen && p[j + 1] == '*') {
        // Case with '*' in pattern
        result = (firstMatch && isMatchHelper(s, p, i + 1, j)) || isMatchHelper(s, p, i, j + 2);
    } else {
        // Regular character match
        result = firstMatch && isMatchHelper(s, p, i + 1, j + 1);
    }

    cache[i][j] = result; // Store result in cache
    return result;
}

// Main function to check if `s` matches `p`
bool isMatch(const char* s, const char* p) {
    int sLen = strlen(s);
    int pLen = strlen(p);
    initializeCache(sLen, pLen);
    bool result = isMatchHelper(s, p, 0, 0);

    // Free memory allocated for cache
    for (int i = 0; i <= sLen; i++) {
        free(cache[i]);
    }
    free(cache);

    return result;
}
```