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

```typescript
import { ListNode } from '../../com_github_leetcode/listnode'

/*
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */
const merge2Lists = (list1: ListNode | null, list2: ListNode | null): ListNode | null => {
    if (!list1 || !list2) {
        return list1 ?? list2
    }
    const tempHead = new ListNode()
    let current = tempHead
    let l1 = list1
    let l2 = list2
    while (l1 || l2) {
        if (!l1) {
            current.next = l2
            break
        }
        if (!l2) {
            current.next = l1
            break
        }
        if (l1.val < l2.val) {
            current.next = l1
            l1 = l1.next
        } else {
            current.next = l2
            l2 = l2.next
        }
        current = current.next
    }
    return tempHead.next
}

const mergeKLists = (lists: Array<ListNode | null>): ListNode | null => {
    while (lists.length > 1) {
        const mergedLists = []
        for (let i = 0; i < lists.length; i += 2) {
            const list1 = lists[i]
            const list2 = lists[i + 1] ?? null
            mergedLists.push(merge2Lists(list1, list2))
        }
        lists = mergedLists
    }
    return lists[0] ?? null
}

export { mergeKLists }
```