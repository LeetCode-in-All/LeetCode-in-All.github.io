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

```typescript
import { ListNode } from '../../com_github_leetcode/listnode'

let localN: number

function removeNthFromEnd(head: ListNode | null, n: number): ListNode | null {
    localN = n
    const dummy = new ListNode(0)
    dummy.next = head
    removeNth(dummy)
    return dummy.next
}

function removeNth(node: ListNode | null): void {
    if (!node || !node.next) { //NOSONAR
        return
    }
    removeNth(node.next)
    localN--

    if (localN === 0) {
        node.next = node.next?.next || null //NOSONAR
    }
}

export { removeNthFromEnd }
```