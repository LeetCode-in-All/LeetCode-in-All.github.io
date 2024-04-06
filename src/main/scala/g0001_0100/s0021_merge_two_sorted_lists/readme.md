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
    def mergeTwoLists(l1: ListNode, l2: ListNode): ListNode = {
        var list: ListNode = new ListNode(-1)
        val head: ListNode = list
        var l1Temp: ListNode = l1
        var l2Temp: ListNode = l2
        while (l1Temp != null || l2Temp != null) {
            if (l1Temp != null && l2Temp != null) {
                if (l1Temp.x <= l2Temp.x) {
                    list.next = new ListNode(l1Temp.x)
                    l1Temp = l1Temp.next
                } else {
                    list.next = new ListNode(l2Temp.x)
                    l2Temp = l2Temp.next
                }
            } else if (l1Temp != null) {
                list.next = new ListNode(l1Temp.x)
                l1Temp = l1Temp.next
            } else {
                list.next = new ListNode(l2Temp.x)
                l2Temp = l2Temp.next
            }
            list = list.next
        }
        head.next
    }
}
```