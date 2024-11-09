[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 21\. Merge Two Sorted Lists

Easy

Merge two sorted linked lists and return it as a **sorted** list. The list should be made by splicing together the nodes of the first two lists.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

**Input:** l1 = [1,2,4], l2 = [1,3,4]

**Output:** [1,1,2,3,4,4]

**Example 2:**

**Input:** l1 = [], l2 = []

**Output:** []

**Example 3:**

**Input:** l1 = [], l2 = [0]

**Output:** [0]

**Constraints:**

*   The number of nodes in both lists is in the range `[0, 50]`.
*   `-100 <= Node.val <= 100`
*   Both `l1` and `l2` are sorted in **non-decreasing** order.

## Solution

```c
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
struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2) {
    struct ListNode dummy = {-1, NULL};  // Dummy head node
    struct ListNode* list = &dummy;      // Pointer to the dummy node

    while (l1 != NULL || l2 != NULL) {
        if (l1 != NULL && l2 != NULL) {
            if (l1->val <= l2->val) {
                list->next = createNode(l1->val);
                l1 = l1->next;
            } else {
                list->next = createNode(l2->val);
                l2 = l2->next;
            }
        } else if (l1 != NULL) {
            list->next = createNode(l1->val);
            l1 = l1->next;
        } else {
            list->next = createNode(l2->val);
            l2 = l2->next;
        }
        list = list->next;
    }

    return dummy.next;  // Return the merged list starting from dummy's next node
}
```