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
    def sortList(head: ListNode): ListNode = {
        if (head == null || head.next == null) {
            return head
        }
        val (first, second) = splitList(head)
        mergeLists(sortList(first), sortList(second))
    }

    def splitList(head: ListNode): (ListNode, ListNode) = {
        var slow = head
        var fast = head
        var pre = slow
        while (fast != null && fast.next != null) {
            pre = slow
            slow = slow.next
            fast = fast.next.next
        }
        pre.next = null
        (head, slow)
    }

    private def mergeLists(first: ListNode, second: ListNode): ListNode = {
        val res = new ListNode(0)
        var cur = res
        var (firstPtr, secondPtr) = (first, second)

        while (firstPtr != null || secondPtr != null) {
            if (firstPtr != null && (secondPtr == null || firstPtr.x <= secondPtr.x)) {
                cur.next = firstPtr
                firstPtr = firstPtr.next
            } else {
                cur.next = secondPtr
                secondPtr = secondPtr.next
            }
            cur = cur.next
        }

        res.next
    }
}
```