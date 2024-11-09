[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 647\. Palindromic Substrings

Medium

Given a string `s`, return _the number of **palindromic substrings** in it_.

A string is a **palindrome** when it reads the same backward as forward.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "abc"

**Output:** 3

**Explanation:** Three palindromic strings: "a", "b", "c".

**Example 2:**

**Input:** s = "aaa"

**Output:** 6

**Explanation:** Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consists of lowercase English letters.

## Solution

```c
int isRepeat(char*s , int idx, int len, int* counter) {
    int tmp = idx + 1;
    while(tmp < len && s[tmp] == s[idx]) tmp++;
    *counter += ((tmp-idx)*(tmp-idx-1))/2;

    return tmp;
}

int isPalindrome(char* s, int idx, int len, int* counter) {
    int end = isRepeat(s, idx, len, counter);
    int ret = end;
    int start = idx - 1;
    while(start >= 0 && end < len && s[start--] == s[end++]) (*counter)++;
    
    return ret;
}

int countSubstrings(char* s) {
    int len = strlen(s);
    int counter = len;
    int idx = 0;
    while(idx < len) idx = isPalindrome(s, idx, len, &counter);

    return counter;
}
```