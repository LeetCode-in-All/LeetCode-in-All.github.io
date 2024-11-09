[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 24\. Swap Nodes in Pairs

Medium

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)

**Input:** head = [1,2,3,4]

**Output:** [2,1,4,3]

**Example 2:**

**Input:** head = []

**Output:** []

**Example 3:**

**Input:** head = [1]

**Output:** [1]

**Constraints:**

*   The number of nodes in the list is in the range `[0, 100]`.
*   `0 <= Node.val <= 100`

## Solution

```c
#include <stdio.h>
#include <stdlib.h>

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
// Function to create a new ListNode
struct ListNode* createNode(int val) {
    struct ListNode* node = (struct ListNode*)malloc(sizeof(struct ListNode));
    node->val = val;
    node->next = NULL;
    return node;
}

// Function to calculate the length of the linked list
int getLength(struct ListNode* curr) {
    int cnt = 0;
    while (curr != NULL) {
        cnt++;
        curr = curr->next;
    }
    return cnt;
}

// Recursive function to reverse nodes in pairs
struct ListNode* reverse(struct ListNode* head, int len) {
    // Base case: if there are less than 2 nodes, return the head
    if (len < 2) {
        return head;
    }

    struct ListNode* curr = head;
    struct ListNode* prev = NULL;
    struct ListNode* next;

    // Reverse the first 2 nodes
    for (int i = 0; i < 2; i++) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }

    // Set the next pointer of the last node in the reversed pair to the result of the next reverse call
    head->next = reverse(curr, len - 2);

    return prev;
}

// Main function to swap nodes in pairs
struct ListNode* swapPairs(struct ListNode* head) {
    if (head == NULL) {
        return NULL;
    }
    int len = getLength(head);
    return reverse(head, len);
}
```