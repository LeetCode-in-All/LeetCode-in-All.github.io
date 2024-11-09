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

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_COMBINATIONS 1000

void findCombinations(int start, const char *digits, const char **letters, char *curr, int depth, char ***ans, int *returnSize) {
    if (depth == strlen(digits)) {
        (*ans)[*returnSize] = strdup(curr);
        (*returnSize)++;
        return;
    }

    for (int i = start; i < strlen(digits); i++) {
        int n = digits[i] - '0';
        for (int j = 0; letters[n][j] != '\0'; j++) {
            curr[depth] = letters[n][j];
            findCombinations(i + 1, digits, letters, curr, depth + 1, ans, returnSize);
        }
    }
}

char **letterCombinations(const char *digits, int *returnSize) {
    if (strlen(digits) == 0) {
        *returnSize = 0;
        return NULL;
    }

    const char *letters[] = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    char **ans = (char **)malloc(MAX_COMBINATIONS * sizeof(char *));
    char *curr = (char *)malloc((strlen(digits) + 1) * sizeof(char));
    curr[strlen(digits)] = '\0';
    int returnCount = 0;

    findCombinations(0, digits, letters, curr, 0, &ans, &returnCount);

    free(curr);
    *returnSize = returnCount;
    return ans;
}
```