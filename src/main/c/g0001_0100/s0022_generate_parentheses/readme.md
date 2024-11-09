[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 22\. Generate Parentheses

Medium

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3

**Output:** ["((()))","(()())","(())()","()(())","()()()"]

**Example 2:**

**Input:** n = 1

**Output:** ["()"]

**Constraints:**

*   `1 <= n <= 8`

## Solution

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int countPossibilities(int open, int closed, int n) {
    if (closed == n) {
        return 1;
    }

    if (open == n) {
        return countPossibilities(open, closed + 1, n);
    }

    if (open == closed) {
        return countPossibilities(open + 1, closed, n);
    }

    return countPossibilities(open + 1, closed, n) + countPossibilities(open, closed + 1, n);
}

void generateParentasis(
    int open,
    int closed,
    int n,
    char* currentString, 
    int currentIndex, 
    char** result, 
    int *resultIndex) {
        
    if (closed == n) {
        result[*resultIndex] = currentString; 
        (*resultIndex)++;
        return;
    }

    if (open == closed) {
        currentString[currentIndex] = '(';
        generateParentasis(open + 1, closed, n, currentString, currentIndex + 1, result, resultIndex);
        return;
    }

    if (open == n) {
        currentString[currentIndex] = ')';
        generateParentasis(open, closed + 1, n, currentString, currentIndex + 1, result, resultIndex);
        return;
    }

    char* duplicatedString = malloc(sizeof(char) * (n * 2 + 1));
    strcpy(duplicatedString, currentString);
    currentString[currentIndex] = '(';
    generateParentasis(open + 1, closed, n, currentString, currentIndex + 1, result, resultIndex);
    duplicatedString[currentIndex] = ')';
    generateParentasis(open, closed + 1, n, duplicatedString, currentIndex + 1, result, resultIndex);
}

char** generateParenthesis(int n, int* returnSize) {
    *returnSize = countPossibilities(0, 0, n);
    char** result = malloc(sizeof(char*) * (*returnSize));
    int resultIndex = 0;
    char * currentString = malloc(sizeof(char) * (n * 2 + 1));
    currentString[n * 2] = '\0';
    generateParentasis(0, 0, n, currentString, 0, result, &resultIndex);
    return result;
}
```