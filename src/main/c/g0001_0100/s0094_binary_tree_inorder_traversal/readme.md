[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 94\. Binary Tree Inorder Traversal

Easy

Given the `root` of a binary tree, return _the inorder traversal of its nodes' values_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

**Input:** root = [1,null,2,3]

**Output:** [1,3,2] 

**Example 2:**

**Input:** root = []

**Output:** [] 

**Example 3:**

**Input:** root = [1]

**Output:** [1] 

**Example 4:**

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_5.jpg)

**Input:** root = [1,2]

**Output:** [2,1] 

**Example 5:**

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_4.jpg)

**Input:** root = [1,null,2]

**Output:** [1,2] 

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 100]`.
*   `-100 <= Node.val <= 100`

**Follow up:** Recursive solution is trivial, could you do it iteratively?

## Solution

```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
#define INIT_STACK_CAPACITY 2
#define EMPTY_INDEX -1

typedef struct stack {
    int topIndex;
    int capacity;
    struct TreeNode** datas;
} Stack;

Stack* createStack() {
    Stack *s = (Stack*)malloc(sizeof(Stack));
    s->topIndex = EMPTY_INDEX;
    s->capacity = INIT_STACK_CAPACITY;
    s->datas = (struct TreeNode**)malloc(s->capacity * sizeof(struct TreeNode*));
    for (int i = 0; i < s->capacity; i++) {
        s->datas[i] = NULL;
    }
    return s;
}

bool isFullStack(Stack *s) {
    return(s->topIndex >= (s->capacity - 1));
}

bool isEmptyStack(Stack *s) {
    return(s->topIndex == EMPTY_INDEX);
}

void push(Stack *s, struct TreeNode* node) {
    if (isFullStack(s)) {
        s->capacity *= 2;
        s->datas = (struct TreeNode**)realloc(s->datas, s->capacity * sizeof(struct TreeNode*));
        for (int i = (s->topIndex + 1); i < s->capacity; i++) {
            s->datas[i] = NULL;
        }
    }
    s->datas[++(s->topIndex)] = node;
}

struct TreeNode* pop(Stack* s) {
    if (isEmptyStack(s)) {
        return NULL;
    }
    return s->datas[s->topIndex--];
}

struct TreeNode* top(Stack* s) {
    if (isEmptyStack(s)) {
        return NULL;
    }
    return s->datas[s->topIndex];
}

int size(Stack* s) {
    return s->topIndex + 1;
}

void freeStack(Stack* s) {
    for (int i = 0; i < s->capacity; i++) {
        free(s->datas[i]);
    }
    free(s->datas);
    free(s);
}

int* inorderTraversal(struct TreeNode* root, int* returnSize) {
    Stack *s = createStack();
    *returnSize = 0;
    int* ans = (int*)malloc(200*sizeof(int));

    while (root || !isEmptyStack(s)) {
        if (root) {
            push(s, root);
            root = root->left;
        } else {
            root = pop(s);
            ans[(*returnSize)++] = root->val;
            root = root->right;
        }
    }
    
    freeStack(s);
    ans = (int*)realloc(ans, *returnSize * sizeof(int));
    return ans;
}
```