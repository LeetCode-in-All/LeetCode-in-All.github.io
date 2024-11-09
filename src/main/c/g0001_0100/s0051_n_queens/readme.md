[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 51\. N-Queens

Hard

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _all distinct solutions to the **n-queens puzzle**_. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

**Input:** n = 4

**Output:** [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]

**Explanation:** There exist two distinct solutions to the 4-queens puzzle as shown above

**Example 2:**

**Input:** n = 1

**Output:** [["Q"]]

**Constraints:**

*   `1 <= n <= 9`

## Solution

```c
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
void mark(int n, int** checkerboard, int i, int j){
    int left = j;
    int right = j;
    i++;
    right++;
    left--;
    while (i < n){
        if (right < n){
            checkerboard[i][right]++;
            right++;
        }
        if (left >= 0){
            checkerboard[i][left]++;
            left--;
        }
        checkerboard[i][j]++;
        i++;
    }
    return;
}

void del_mark(int n, int** checkerboard, int i, int j){
    int left = j;
    int right = j;
    i++;
    right++;
    left--;
    while (i < n){
        if (right < n){
            checkerboard[i][right]--;
            right++;
        }
        if (left >= 0){
            checkerboard[i][left]--;
            left--;
        }
        checkerboard[i][j]--;
        i++;
    }
    return;
}

void check(int** checkerboard, int n, int* returnSize, int i, char*** ans, int** returnColumnSizes, int* location){
    if (i == n){
        ans[*returnSize] = malloc(sizeof(char*)*n);
        for (int k = 0 ; k < n ; k++){
            ans[*returnSize][k] = malloc(sizeof(char)*(n+1));
            for (int t = 0 ; t < n ; t++){
                if (t == location[k]){
                    ans[*returnSize][k][t] = 'Q';
                } else ans[*returnSize][k][t] = '.';
            }
            ans[*returnSize][k][n] = '\0';
        }
        (*returnColumnSizes)[*returnSize] = n;
        *returnSize += 1;
        return;
    }
    for (int j = 0 ; j < n ; j++){
        if (checkerboard[i][j] == 0){
            mark( n, checkerboard, i, j);
            location[i] = j;
            check(checkerboard, n, returnSize, i+1, ans, returnColumnSizes, location);
            del_mark( n, checkerboard, i, j);
        } 
    }
}

char *** solveNQueens(int n, int* returnSize, int** returnColumnSizes){
    char*** ans = malloc(sizeof(char**)*352);
    (*returnColumnSizes) = malloc(sizeof(int)*352);
    int location[10];
    int** checkerboard = malloc(sizeof(int*)*n);
    for (int i = 0 ; i < n ; i++){
        checkerboard[i] = calloc(n,sizeof(int));
    }
    *returnSize = 0;
    check(checkerboard, n, returnSize, 0, ans, returnColumnSizes, location);
    for (int i = 0 ; i < n ; i++){
        free(checkerboard[i]);
    }
    free(checkerboard);
    return ans;
}
```