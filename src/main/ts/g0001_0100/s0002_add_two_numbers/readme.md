[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 2\. Add Two Numbers

Medium

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

**Input:** l1 = [2,4,3], l2 = [5,6,4]

**Output:** [7,0,8]

**Explanation:** 342 + 465 = 807. 

**Example 2:**

**Input:** l1 = [0], l2 = [0]

**Output:** [0] 

**Example 3:**

**Input:** l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]

**Output:** [8,9,9,9,0,0,0,1] 

**Constraints:**

*   The number of nodes in each linked list is in the range `[1, 100]`.
*   `0 <= Node.val <= 9`
*   It is guaranteed that the list represents a number that does not have leading zeros.

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
function addTwoNumbers(l1: ListNode | null, l2: ListNode | null): ListNode | null {
    const dummyHead: ListNode = new ListNode(0)
    let p: ListNode | null = l1
    let q: ListNode | null = l2
    let curr: ListNode | null = dummyHead
    let carry: number = 0
    while (p !== null || q !== null) {
        const x: number = p !== null ? p.val : 0
        const y: number = q !== null ? q.val : 0
        const sum: number = carry + x + y
        carry = Math.floor(sum / 10)
        curr.next = new ListNode(sum % 10)
        curr = curr.next
        if (p !== null) {
            p = p.next
        }
        if (q !== null) {
            q = q.next
        }
    }
    if (carry > 0) {
        curr.next = new ListNode(carry)
    }
    return dummyHead.next
}

export { addTwoNumbers }
```