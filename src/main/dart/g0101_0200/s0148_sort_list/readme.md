[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 148\. Sort List

Medium

Given the `head` of a linked list, return _the list after sorting it in **ascending order**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg)

**Input:** head = [4,2,1,3]

**Output:** [1,2,3,4]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg)

**Input:** head = [-1,5,3,4,0]

**Output:** [-1,0,3,4,5]

**Example 3:**

**Input:** head = []

**Output:** []

**Constraints:**

*   The number of nodes in the list is in the range <code>[0, 5 * 10<sup>4</sup>]</code>.
*   <code>-10<sup>5</sup> <= Node.val <= 10<sup>5</sup></code>

**Follow up:** Can you sort the linked list in `O(n logn)` time and `O(1)` memory (i.e. constant space)?

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
  ListNode? sortList(ListNode? head) {
    if (head == null || head.next == null) return head;

    // Get the middle of the list and split it into two halves
    ListNode? mid = getMidNode(head);

    // Recursively sort both halves
    ListNode? left = sortList(head);
    ListNode? right = sortList(mid);

    // Merge the sorted halves
    return mergeLists(left, right);
  }

  ListNode? mergeLists(ListNode? node1, ListNode? node2) {
    ListNode dummyHead = ListNode(); // Use a dummy node
    ListNode? tail = dummyHead;

    while (node1 != null && node2 != null) {
      if (node1.val <= node2.val) {
        tail?.next = node1;
        node1 = node1.next;
      } else {
        tail?.next = node2;
        node2 = node2.next;
      }
      tail = tail?.next;
    }

    // Append the remaining nodes
    tail?.next = (node1 != null) ? node1 : node2;
    return dummyHead.next;
  }

  ListNode? getMidNode(ListNode? head) {
    ListNode? fast = head;
    ListNode? slow = head;
    ListNode? prevSlow; // To disconnect the first half

    while (fast != null && fast.next != null) {
      prevSlow = slow;
      slow = slow?.next;
      fast = fast.next?.next;
    }

    // Disconnect the first half from the second half
    prevSlow?.next = null;
    return slow;
  }
}
```