[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 23\. Merge k Sorted Lists

Hard

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

_Merge all the linked-lists into one sorted linked-list and return it._

**Example 1:**

**Input:** lists = \[\[1,4,5],[1,3,4],[2,6]]

**Output:** [1,1,2,3,4,4,5,6]

**Explanation:** The linked-lists are: [ 1->4->5, 1->3->4, 2->6 ] merging them into one sorted list: 1->1->2->3->4->4->5->6

**Example 2:**

**Input:** lists = []

**Output:** []

**Example 3:**

**Input:** lists = \[\[]]

**Output:** []

**Constraints:**

*   `k == lists.length`
*   `0 <= k <= 10^4`
*   `0 <= lists[i].length <= 500`
*   `-10^4 <= lists[i][j] <= 10^4`
*   `lists[i]` is sorted in **ascending order**.
*   The sum of `lists[i].length` won't exceed `10^4`.

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

// Function to merge two sorted linked lists
struct ListNode* mergeTwoLists(struct ListNode* left, struct ListNode* right) {
    if (left == NULL) return right;
    if (right == NULL) return left;

    struct ListNode* res;
    if (left->val <= right->val) {
        res = left;
        left = left->next;
    } else {
        res = right;
        right = right->next;
    }

    struct ListNode* node = res;
    while (left != NULL || right != NULL) {
        if (left == NULL) {
            node->next = right;
            right = right->next;
        } else if (right == NULL) {
            node->next = left;
            left = left->next;
        } else {
            if (left->val <= right->val) {
                node->next = left;
                left = left->next;
            } else {
                node->next = right;
                right = right->next;
            }
        }
        node = node->next;
    }
    return res;
}

// Recursive function to merge k sorted lists
struct ListNode* mergeKListsHelper(struct ListNode** lists, int leftIndex, int rightIndex) {
    if (rightIndex > leftIndex + 1) {
        int mid = (leftIndex + rightIndex) / 2;
        struct ListNode* left = mergeKListsHelper(lists, leftIndex, mid);
        struct ListNode* right = mergeKListsHelper(lists, mid, rightIndex);
        return mergeTwoLists(left, right);
    } else {
        return lists[leftIndex];
    }
}

// Function to initiate mergeKLists with bounds
struct ListNode* mergeKLists(struct ListNode** lists, int listsSize) {
    if (listsSize == 0) return NULL;
    return mergeKListsHelper(lists, 0, listsSize);
}
```