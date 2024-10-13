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

```dart
/**
 * Definition for singly-linked list.
 * class ListNode {
 *   int val;
 *   ListNode? next;
 *   ListNode([this.val = 0, this.next]);
 * }
 */
class Solution {
  ListNode? swapPairs(ListNode? head) {
    if (head == null) {
      return null;
    }
    int len = getLength(head);
    return reverse(head, len);
  }

  // Function to get the length of the linked list
  int getLength(ListNode? curr) {
    int cnt = 0;
    while (curr != null) {
      cnt++;
      curr = curr.next;
    }
    return cnt;
  }

  // Recursive function to reverse pairs of nodes
  ListNode? reverse(ListNode? head, int len) {
    // Base case: if less than 2 nodes, no need to swap
    if (len < 2) {
      return head;
    }
    ListNode? curr = head;
    ListNode? prev;
    ListNode? next;
    prev = null;

    // Reverse the first two nodes
    for (int i = 0; i < 2; i++) {
      next = curr!.next;
      curr.next = prev;
      prev = curr;
      curr = next;
    }

    // Recursively reverse the rest of the list
    head!.next = reverse(curr, len - 2);
    return prev;
  }
}
```