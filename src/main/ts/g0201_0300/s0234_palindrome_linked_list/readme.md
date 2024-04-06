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

```typescript
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
function isPalindrome(head: ListNode | null): boolean {
    if (head === null || head.next === null) {
        // Empty list or single element is considered a palindrome.
        return true
    }
    let len = 0
    let right = head
    // Calculate the length of the list.
    while (right !== null) {
        right = right.next
        len++
    }
    // Find the middle of the list.
    let middle = Math.floor(len / 2)
    // Reset the right pointer to the head.
    right = head
    // Move the right pointer to the middle of the list.
    for (let i = 0; i < middle; i++) {
        right = right.next
    }
    // Reverse the right half of the list.
    let prev = null
    while (right !== null) {
        const next = right.next
        right.next = prev
        prev = right
        right = next
    }
    // Compare the left and right halves.
    for (let i = 0; i < middle; i++) {
        if (prev !== null && head.val === prev.val) {
            head = head.next
            prev = prev.next
        } else {
            return false
        }
    }
    return true
}

export { isPalindrome }
```