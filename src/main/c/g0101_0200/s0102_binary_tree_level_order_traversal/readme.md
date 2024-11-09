[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 102\. Binary Tree Level Order Traversal

Medium

Given the `root` of a binary tree, return _the level order traversal of its nodes' values_. (i.e., from left to right, level by level).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = [3,9,20,null,null,15,7]

**Output:** [[3],[9,20],[15,7]]

**Example 2:**

**Input:** root = [1]

**Output:** [[1]]

**Example 3:**

**Input:** root = []

**Output:** []

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 2000]`.
*   `-1000 <= Node.val <= 1000`

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
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *returnColumnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
typedef struct QueueNode {
    struct TreeNode* node;
    struct QueueNode* next;
} QueueNode;

struct Queue {
    QueueNode* head;
    QueueNode* tail;
    int size;
};

QueueNode* createQueueNode(struct TreeNode* node);
void enqueue(struct Queue* Queue, struct TreeNode* node);
struct TreeNode* dequeue(struct Queue* Queue);

int** levelOrder(struct TreeNode* root, int* returnSize, int** returnColumnSizes) {
    int** result = malloc(sizeof(int*) * 2000);
    if (!root) {
        *returnSize = 0;
        *returnColumnSizes = NULL;
        return NULL;
    }

    struct Queue Queue;
    Queue.head = Queue.tail = NULL;
    Queue.size = 0;
    enqueue(&Queue, root);

    int levelSize = 1, i = 0;
    *returnColumnSizes = malloc(sizeof(int) * 2000);
    while (Queue.size > 0) {
        (*returnColumnSizes)[i] = levelSize;
        result[i] = malloc(sizeof(int) * levelSize);
        for (int j = 0; j < levelSize; j++) {
            struct TreeNode* node = dequeue(&Queue);
            result[i][j] = node->val;
            if (node->left) {
                enqueue(&Queue, node->left);
            }
            if (node->right) {
                enqueue(&Queue, node->right);
            }
        }
        levelSize = Queue.size;
        i++;
    }
    *returnSize = i;
    return result;
}

struct TreeNode* dequeue(struct Queue* Queue) {
    if (Queue->size == 0) {
        return NULL;
    }
    struct TreeNode* node = Queue->head->node;
    QueueNode* temp = Queue->head;
    Queue->head = Queue->head->next;
    Queue->size--;
    free(temp);
    return node;
}

void enqueue(struct Queue* Queue, struct TreeNode* node) {
    QueueNode* newNode = createQueueNode(node);
    if (Queue->size == 0) {
        Queue->head = newNode;
        Queue->tail = newNode;
        Queue->size++;
        return;
    } else {
        Queue->tail->next = newNode;
        Queue->tail = newNode;
        Queue->size++;
        return;
    }
}

QueueNode* createQueueNode(struct TreeNode* node) {
    QueueNode* newNode = (QueueNode*)malloc(sizeof(QueueNode));
    newNode->node = node;
    newNode->next = NULL;
    return newNode;
}
```