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
        var len = 0
        var right = head

        // Calculate the length
        while (right != null) {
            right = right.next
            len += 1
        }

        // Reverse the right half of the list
        len = len / 2
        right = head
        for (_ <- 0 until len) {
            right = right.next
        }

        var prev: ListNode = null
        while (right != null) {
            val next = right.next
            right.next = prev
            prev = right
            right = next
        }
        var head2 = head
        // Compare left half and right half
        for (_ <- 0 until len) {
            if (prev != null && head2.x == prev.x) {
                head2 = head2.next
                prev = prev.next
            } else {
                return false
            }
        }

        true
    }
}
```