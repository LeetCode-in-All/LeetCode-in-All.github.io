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

```csharp
using LeetCodeNet.Com_github_leetcode;

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    private int n;

    public ListNode RemoveNthFromEnd(ListNode head, int n) {
        this.n = n;
        ListNode node = new ListNode(0, head);
        RemoveNth(node);
        return node.next;
    }

    private void RemoveNth(ListNode node) {
        if (node.next == null) {
            return;
        }
        RemoveNth(node.next);
        this.n--;
        if (this.n == 0) {
            node.next = node.next.next;
        }
    }
}
```