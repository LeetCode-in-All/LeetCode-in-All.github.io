[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 6\. Zigzag Conversion

Medium

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P A H N A P L S I I G Y I R 

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

string convert(string s, int numRows); 

**Example 1:**

**Input:** s = "PAYPALISHIRING", numRows = 3

**Output:** "PAHNAPLSIIGYIR" 

**Example 2:**

**Input:** s = "PAYPALISHIRING", numRows = 4

**Output:** "PINALSIGYAHRPI"

**Explanation:** P I N A L S I G Y A H R P I 

**Example 3:**

**Input:** s = "A", numRows = 1

**Output:** "A" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consists of English letters (lower-case and upper-case), `','` and `'.'`.
*   `1 <= numRows <= 1000`

## Solution

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char* convert(const char* s, int numRows) {
    int sLen = strlen(s);
    if (numRows == 1) {
        // Return a copy of s since the function is expected to return a new string
        char* result = (char*)malloc((sLen + 1) * sizeof(char));
        strcpy(result, s);
        return result;
    }

    int maxDist = numRows * 2 - 2;
    char* buf = (char*)malloc((sLen + 1) * sizeof(char));
    int bufIndex = 0; // Keeps track of current position in buffer

    for (int i = 0; i < numRows; i++) {
        int index = i;
        if (i == 0 || i == numRows - 1) {
            // For the first and last rows
            while (index < sLen) {
                buf[bufIndex++] = s[index];
                index += maxDist;
            }
        } else {
            // For the middle rows
            while (index < sLen) {
                buf[bufIndex++] = s[index];
                index += maxDist - i * 2;
                if (index >= sLen) {
                    break;
                }
                buf[bufIndex++] = s[index];
                index += i * 2;
            }
        }
    }

    buf[bufIndex] = '\0';
    return buf;
}
```