[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 19\. Remove Nth Node From End of List

Medium

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

**Input:** head = [1,2,3,4,5], n = 2

**Output:** [1,2,3,5]

**Example 2:**

**Input:** head = [1], n = 1

**Output:** []

**Example 3:**

**Input:** head = [1,2], n = 1

**Output:** [1]

**Constraints:**

*   The number of nodes in the list is `sz`.
*   `1 <= sz <= 30`
*   `0 <= Node.val <= 100`
*   `1 <= n <= sz`

**Follow up:** Could you do this in one pass?

## Solution

```c
#include <stdio.h>
#include <stdlib.h>

struct Solution {
    int n;
};

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* removeNthFromEnd(struct ListNode* head, int n) {
    struct Solution solution;
    solution.n = n;
    
    // Create a new dummy node pointing to the head
    struct ListNode* dummy = (struct ListNode*)malloc(sizeof(struct ListNode));
    dummy->val = 0; // Value is not important for dummy
    dummy->next = head;
    
    // Call the recursive function to remove the Nth node
    removeNth(dummy, &solution);
    
    // Store the new head and free the dummy node
    struct ListNode* newHead = dummy->next;
    free(dummy);
    
    return newHead;
}

void removeNth(struct ListNode* node, struct Solution* solution) {
    if (node->next == NULL) {
        return; // Base case
    }
    
    removeNth(node->next, solution);
    solution->n--;

    if (solution->n == 0) {
        struct ListNode* toDelete = node->next; // Node to be deleted
        node->next = node->next->next; // Skip the node
        free(toDelete); // Free the memory of the deleted node
    }
}

// Function to create a new ListNode
struct ListNode* createNode(int value) {
    struct ListNode* newNode = (struct ListNode*)malloc(sizeof(struct ListNode));
    newNode->val = value;
    newNode->next = NULL;
    return newNode;
}
```