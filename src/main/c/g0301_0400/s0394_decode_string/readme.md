[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 394\. Decode String

Medium

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed <code>10<sup>5</sup></code>.

**Example 1:**

**Input:** s = "3[a]2[bc]"

**Output:** "aaabcbc"

**Example 2:**

**Input:** s = "3[a2[c]]"

**Output:** "accaccacc"

**Example 3:**

**Input:** s = "2[abc]3[cd]ef"

**Output:** "abcabccdcdcdef"

**Constraints:**

*   `1 <= s.length <= 30`
*   `s` consists of lowercase English letters, digits, and square brackets `'[]'`.
*   `s` is guaranteed to be **a valid** input.
*   All the integers in `s` are in the range `[1, 300]`.

## Solution

```c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <string.h>

// Helper function to repeat a string a given number of times
char* repeatString(const char* str, int count) {
    int len = strlen(str);
    char* result = (char*)malloc(len * count + 1);
    result[0] = '\0'; // Start with an empty string
    
    for (int i = 0; i < count; i++) {
        strcat(result, str);
    }
    return result;
}

// Helper function for recursive decoding
char* decodeHelper(char* s, int* pos) {
    char* result = (char*)malloc(10000); // Allocate sufficient space for result
    result[0] = '\0'; // Initialize as an empty string
    int count = 0;

    while (s[*pos] != '\0') {
        char c = s[*pos];
        (*pos)++;

        if (isalpha(c)) {
            // If it's a letter, append it to the result
            int len = strlen(result);
            result[len] = c;
            result[len + 1] = '\0';
        } else if (isdigit(c)) {
            // If it's a digit, accumulate it as part of count
            count = count * 10 + (c - '0');
        } else if (c == '[') {
            // Start of a nested encoded string
            char* decodedSubstring = decodeHelper(s, pos);
            char* repeatedSubstring = repeatString(decodedSubstring, count);
            strcat(result, repeatedSubstring);
            free(decodedSubstring);
            free(repeatedSubstring);
            count = 0; // Reset count after using it
        } else if (c == ']') {
            // End of the current encoded substring
            break;
        }
    }
    return result;
}

// Main function to decode the string
char* decodeString(char* s) {
    int pos = 0;
    return decodeHelper(s, &pos);
}
```