[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 131\. Palindrome Partitioning

Medium

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

**Example 1:**

**Input:** s = "aab"

**Output:** [["a","a","b"],["aa","b"]]

**Example 2:**

**Input:** s = "a"

**Output:** [["a"]]

**Constraints:**

*   `1 <= s.length <= 16`
*   `s` contains only lowercase English letters.

## Solution

```c
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int isPalindrome(char *s, int start, int end) {
    while (start <= end) {
        if (s[start] != s[end]) {
            return 0;
        }
        start++;
        end--;
    }
    return 1;
}

char ***partition(char *s, int *returnSize, int **returnColumnSizes) {
    int str_len = strlen(s);
    int all_pos_cnt = 1 << (str_len - 1); // Count for all possible substring partitions
    char ***ret = calloc(all_pos_cnt, sizeof(char **));
    *returnSize = 0;

    *returnColumnSizes = calloc(all_pos_cnt, sizeof(int));

    for (int sel_bit = 0; sel_bit < all_pos_cnt; sel_bit++) {
        char **substr = calloc(str_len, sizeof(char *));
        int start = 0;
        int sub_idx = 0;
        int valid = 1;

        for (int ith_b = 0; ith_b < (str_len - 1); ith_b++) {
            if (((1 << ith_b) & sel_bit) > 0) {
                if (isPalindrome(s, start, ith_b) == 1) {
                    substr[sub_idx] = calloc((ith_b - start + 1 + 1), sizeof(char)); // +1 for '\0'
                    memcpy(&substr[sub_idx][0], &s[start], (ith_b - start + 1) * sizeof(char));
                    substr[sub_idx][ith_b - start + 1] = '\0';
                    start = ith_b + 1;
                    sub_idx++;
                } else {
                    valid = 0;
                    break;
                }
            }
        }

        if (isPalindrome(s, start, str_len - 1) == 1) { // Check the last part
            substr[sub_idx] = calloc((str_len - start + 1), sizeof(char));
            memcpy(&substr[sub_idx][0], &s[start], (str_len - start) * sizeof(char));
            substr[sub_idx][str_len - start] = '\0';
            sub_idx++;
        } else {
            valid = 0;
        }

        if (valid == 1) {
            ret[*returnSize] = substr;
            (*returnColumnSizes)[*returnSize] = sub_idx;
            (*returnSize)++;
        } else {
            // Free allocated memory for substr if invalid partition
            for (int i = 0; i < sub_idx; i++) {
                free(substr[i]);
            }
            free(substr);
        }
    }

    return ret;
}
```