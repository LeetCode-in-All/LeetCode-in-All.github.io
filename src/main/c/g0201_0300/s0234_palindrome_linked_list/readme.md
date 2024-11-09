[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 234\. Palindrome Linked List

Easy

Given the `head` of a singly linked list, return `true` _if it is a palindrome or_ `false` _otherwise_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

**Input:** head = [1,2,2,1]

**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

**Input:** head = [1,2]

**Output:** false

**Constraints:**

*   The number of nodes in the list is in the range <code>[1, 10<sup>5</sup>]</code>.
*   `0 <= Node.val <= 9`

**Follow up:** Could you do it in `O(n)` time and `O(1)` space?

## Solution

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
#include <stdbool.h>

// Function to check if the linked list is a palindrome
bool isPalindrome(struct ListNode* head) {
    if (head == NULL || head->next == NULL) {
        return true;
    }

    // Step 1: Calculate the length of the list
    int len = 0;
    struct ListNode* right = head;
    while (right != NULL) {
        right = right->next;
        len++;
    }

    // Step 2: Find the middle of the list and reverse the right half
    len = len / 2;
    right = head;
    for (int i = 0; i < len; i++) {
        right = right->next;
    }

    // Reverse the right half of the list
    struct ListNode* prev = NULL;
    while (right != NULL) {
        struct ListNode* next = right->next;
        right->next = prev;
        prev = right;
        right = next;
    }

    // Step 3: Compare the left half and the reversed right half
    struct ListNode* left = head;
    while (prev != NULL) {
        if (left->val != prev->val) {
            return false;
        }
        left = left->next;
        prev = prev->next;
    }

    return true;
}
```