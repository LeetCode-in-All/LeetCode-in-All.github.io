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

```scala
import com_github_leetcode.ListNode

/*
 * Definition for singly-linked list.
 * class ListNode(_x: Int = 0, _next: ListNode = null) {
 *   var next: ListNode = _next
 *   var x: Int = _x
 * }
 */
object Solution {
    def swapPairs(head: ListNode): ListNode = {
        if (head == null) {
            return null
        }
        val len = getLength(head)
        reverse(head, len)
    }

    private def getLength(curr: ListNode): Int = {
        var cnt = 0
        var current = curr
        while (current != null) {
            cnt += 1
            current = current.next
        }
        cnt
    }

    private def reverse(head: ListNode, len: Int): ListNode = {
        if (len < 2) {
            return head
        }
        var curr = head
        var prev: ListNode = null
        var next: ListNode = null
        for (i <- 0 until 2) {
            next = curr.next
            curr.next = prev
            prev = curr
            curr = next
        }
        head.next = reverse(curr, len - 2)
        prev
    }
}
```