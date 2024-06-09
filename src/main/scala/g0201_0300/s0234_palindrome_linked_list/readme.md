[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 234\. Palindrome Linked List

Easy

Given the `head` of a singly linked list, return `true` if it is a palindrome.

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
    def isPalindrome(head: ListNode): Boolean = {
        if (head == null || head.next == null) {
            return true
        }
        def reverseList(node: ListNode): ListNode = {
            var prev: ListNode = null
            var current: ListNode = node
            while (current != null) {
                val nextNode = current.next
                current.next = prev
                prev = current
                current = nextNode
            }
            prev
        }

        def findMiddle(node: ListNode): ListNode = {
            var slow = node
            var fast = node
            while (fast != null && fast.next != null) {
                slow = slow.next
                fast = fast.next.next
            }
            slow
        }

        val middle = findMiddle(head)
        var secondHalf = reverseList(middle)

        var firstHalf = head
        while (secondHalf != null) {
            if (firstHalf.x != secondHalf.x) {
                return false
            }
            firstHalf = firstHalf.next
            secondHalf = secondHalf.next
        }
        true
    }
}
```