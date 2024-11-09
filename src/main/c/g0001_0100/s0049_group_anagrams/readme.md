[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 49\. Group Anagrams

Medium

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** strs = ["eat","tea","tan","ate","nat","bat"]

**Output:** [["bat"],["nat","tan"],["ate","eat","tea"]]

**Example 2:**

**Input:** strs = [""]

**Output:** [[""]]

**Example 3:**

**Input:** strs = ["a"]

**Output:** [["a"]]

**Constraints:**

*   <code>1 <= strs.length <= 10<sup>4</sup></code>
*   `0 <= strs[i].length <= 100`
*   `strs[i]` consists of lowercase English letters.

## Solution

```c
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
const char primes[26] = {
    2,  3,  5,  7,  11, 13, 17, 19, 23, 29,
    31, 37, 41, 43, 47, 53, 59, 61, 67, 71,
    73, 79, 83, 89, 97, 101
};

typedef struct node {
    char** str;
    int size;
    int cap;
    double val;
    struct node* left;
    struct node* right;
    struct node* next;
} node;

void insert(node** data, const char* str, const int bucket, node** first, node** last, int* returnSize) {
    double val = 1;
    const char* c = str;
    while (*c) {
        val *= primes[*c++ - 'a'];
    }
    node** branch = &data[(int)fmod(val, bucket)];

    while (*branch) {
        if ((*branch)->val < val) {
            branch = &((*branch)->left);
        } else if (val < (*branch)->val) {
            branch = &((*branch)->right);
        } else {
            if ((*branch)->size == (*branch)->cap) {
                (*branch)->cap *= 4;
                (*branch)->str = (char**)realloc((*branch)->str, (*branch)->cap * sizeof(char*));
            }
            (*branch)->str[(*branch)->size++] = (char*)str;
            return;
        }
    }

    ++(*returnSize);
    *branch = (node*)malloc(sizeof(node));
    (*branch)->size = 1;
    (*branch)->cap = 2;
    (*branch)->val = val;
    (*branch)->left = NULL;
    (*branch)->right = NULL;
    (*branch)->str = (char**)malloc(sizeof(char*) * (*branch)->cap);

    if (*first) {
        (*last)->next = *branch;
    } else {
        *first = *branch;
    }
    *last = *branch;
    (*branch)->str[0] = (char*)str;
}

char*** groupAnagrams(const char** strs, const int strsSize, int* returnSize, int** returnColumnSizes) {
    node** data = (node**)malloc(sizeof(node*) * strsSize);
    for (int i = 0; i < strsSize; i++) {
        data[i] = NULL;
    }

    node* ptr = NULL;
    node* last = NULL;
    *returnSize = 0;
    for (int i = 0; i < strsSize; i++) {
        insert(data, strs[i], strsSize, &ptr, &last, returnSize);
    }

    char*** result = (char***)malloc(sizeof(char**) * (*returnSize));
    *returnColumnSizes = (int*)malloc(sizeof(int) * (*returnSize));

    for (int i = 0; i < *returnSize; i++) {
        last = ptr;
        (*returnColumnSizes)[i] = ptr->size;
        result[i] = ptr->str;
        ptr = ptr->next;
        free(last);
    }

    free(data);
    return result;
}
```