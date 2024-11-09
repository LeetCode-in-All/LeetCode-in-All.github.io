[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 438\. Find All Anagrams in a String

Medium

Given two strings `s` and `p`, return _an array of all the start indices of_ `p`_'s anagrams in_ `s`. You may return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** s = "cbaebabacd", p = "abc"

**Output:** [0,6]

**Explanation:** 

The substring with start index = 0 is "cba", which is an anagram of "abc". 

The substring with start index = 6 is "bac", which is an anagram of "abc".

**Example 2:**

**Input:** s = "abab", p = "ab"

**Output:** [0,1,2]

**Explanation:** 

The substring with start index = 0 is "ab", which is an anagram of "ab". 

The substring with start index = 1 is "ba", which is an anagram of "ab". 

The substring with start index = 2 is "ab", which is an anagram of "ab".

**Constraints:**

*   <code>1 <= s.length, p.length <= 3 * 10<sup>4</sup></code>
*   `s` and `p` consist of lowercase English letters.

## Solution

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
// Helper function to create a dynamic array for storing results
int* createResultArray(int initialSize) {
    return (int*)malloc(initialSize * sizeof(int));
}

// Main function to find all starting indices of p's anagrams in s
int* findAnagrams(const char* s, const char* p, int* returnSize) {
    int map[26] = {0}; // Frequency map for characters in p
    int lenS = strlen(s);
    int lenP = strlen(p);
    int initialSize = 10; // Initial size for result array
    int* result = createResultArray(initialSize);
    *returnSize = 0; // Keeps track of the number of results

    // Populate the frequency map based on string p
    for (int i = 0; i < lenP; ++i) {
        map[p[i] - 'a']++;
    }

    int i = 0, j = 0;
    while (i < lenS) {
        int idx = s[i] - 'a';
        map[idx]--;

        // Adjust the window when it exceeds the length of p
        if (i >= lenP) {
            map[s[j++] - 'a']++;
        }

        // Check if all elements in the map are zero (indicating an anagram)
        bool finish = true;
        for (int k = 0; k < 26; k++) {
            if (map[k] != 0) {
                finish = false;
                break;
            }
        }

        // Add the start index of the anagram to the result if conditions are met
        if (i >= lenP - 1 && finish) {
            if (*returnSize >= initialSize) {
                initialSize *= 2;
                result = realloc(result, initialSize * sizeof(int));
            }
            result[(*returnSize)++] = j;
        }
        i++;
    }
    return result;
}
```