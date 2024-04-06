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
    def mergeKLists(lists: Array[ListNode]): ListNode = {
        if (lists.isEmpty) {
            null
        } else {
            mergeKLists(lists, 0, lists.length)
        }
    }

    def mergeKLists(lists: Array[ListNode], leftIndex: Int, rightIndex: Int): ListNode = {
        if (rightIndex > leftIndex + 1) {
            val mid = (leftIndex + rightIndex) / 2
            val left = mergeKLists(lists, leftIndex, mid)
            val right = mergeKLists(lists, mid, rightIndex)
            mergeTwoLists(left, right)
        } else {
            lists(leftIndex)
        }
    }

    @SuppressWarnings(Array("scala:S1871"))
    def mergeTwoLists(left: ListNode, right: ListNode): ListNode = {
        if (left == null) {
            right
        } else if (right == null) {
            left
        } else {
            var res: ListNode = null
            var (l, r) = (left, right)
            if (l.x <= r.x) {
                res = l
                l = l.next
            } else {
                res = r
                r = r.next
            }
            var node = res
            while (l != null || r != null) {
                if (l == null) {
                    node.next = r
                    r = r.next
                } else if (r == null) {
                    node.next = l
                    l = l.next
                } else if (l.x <= r.x) {
                    node.next = l
                    l = l.next
                } else {
                    node.next = r
                    r = r.next
                }
                node = node.next
            }
            res
        }
    }
}
```