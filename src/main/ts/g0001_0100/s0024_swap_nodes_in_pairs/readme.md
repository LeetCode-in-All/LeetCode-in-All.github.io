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

```typescript
/**
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
function swapPairs(head: ListNode | null): ListNode | null {
    if (head === null) {
        return null
    }
    const len = getLength(head)
    return reverse(head, len)
}

function getLength(curr: ListNode | null): number {
    let cnt = 0
    while (curr !== null) {
        cnt++
        curr = curr.next
    }
    return cnt
}

// Recursive function to reverse in groups
function reverse(head: ListNode | null, len: number): ListNode | null {
    // base case
    if (len < 2) {
        return head
    }
    let curr: ListNode | null = head
    let prev: ListNode | null = null
    let next: ListNode | null
    for (let i = 0; i < 2; i++) {
        // reverse linked list code
        next = curr.next
        curr.next = prev
        prev = curr
        curr = next
    }
    head.next = reverse(curr, len - 2)
    return prev
}

export { swapPairs }
```