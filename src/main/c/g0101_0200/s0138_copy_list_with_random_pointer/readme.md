[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 138\. Copy List with Random Pointer

Medium

A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.

Construct a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) of the list. The deep copy should consist of exactly `n` **brand new** nodes, where each new node has its value set to the value of its corresponding original node. Both the `next` and `random` pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list**.

For example, if there are two nodes `X` and `Y` in the original list, where `X.random --> Y`, then for the corresponding two nodes `x` and `y` in the copied list, `x.random --> y`.

Return _the head of the copied linked list_.

The linked list is represented in the input/output as a list of `n` nodes. Each node is represented as a pair of `[val, random_index]` where:

*   `val`: an integer representing `Node.val`
*   `random_index`: the index of the node (range from `0` to `n-1`) that the `random` pointer points to, or `null` if it does not point to any node.

Your code will **only** be given the `head` of the original linked list.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/12/18/e1.png)

**Input:** head = \[\[7,null],[13,0],[11,4],[10,2],[1,0]]

**Output:** [[7,null],[13,0],[11,4],[10,2],[1,0]]

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/12/18/e2.png)

**Input:** head = \[\[1,1],[2,1]]

**Output:** [[1,1],[2,1]]

**Example 3:**

**![](https://assets.leetcode.com/uploads/2019/12/18/e3.png)**

**Input:** head = \[\[3,null],[3,0],[3,null]]

**Output:** [[3,null],[3,0],[3,null]]

**Constraints:**

*   `0 <= n <= 1000`
*   <code>-10<sup>4</sup> <= Node.val <= 10<sup>4</sup></code>
*   `Node.random` is `null` or is pointing to some node in the linked list.

## Solution

```c
#include <stdlib.h>

/**
 * Definition for a Node.
 * struct Node {
 *     int val;
 *     struct Node *next;
 *     struct Node *random;
 * };
 */

// Helper function to create a new node
struct Node* createNode(int val) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->val = val;
    newNode->next = NULL;
    newNode->random = NULL;
    return newNode;
}

struct Node* copyRandomList(struct Node* head) {
    if (head == NULL) {
        return NULL;
    }

    // First pass: Insert cloned nodes right after each original node.
    struct Node* curr = head;
    while (curr != NULL) {
        struct Node* clonedNode = createNode(curr->val);
        clonedNode->next = curr->next;
        curr->next = clonedNode;
        curr = clonedNode->next;
    }

    // Second pass: Set random pointers for cloned nodes.
    curr = head;
    while (curr != NULL) {
        if (curr->random != NULL) {
            curr->next->random = curr->random->next;
        }
        curr = curr->next->next;
    }

    // Third pass: Separate the original list and cloned list.
    curr = head;
    struct Node* newHead = head->next;
    while (curr != NULL) {
        struct Node* clonedNode = curr->next;
        curr->next = clonedNode->next;
        if (clonedNode->next != NULL) {
            clonedNode->next = clonedNode->next->next;
        }
        curr = curr->next;
    }

    return newHead;
}
```