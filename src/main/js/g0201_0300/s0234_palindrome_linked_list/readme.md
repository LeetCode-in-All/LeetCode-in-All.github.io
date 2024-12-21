[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 234\. Palindrome Linked List

Easy

Given the `head` of a singly linked list, return `true` _if it is a palindrome or_ `false` _otherwise_.

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

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {boolean}
 */
var isPalindrome = function(head) {
    let len = 0
    let right = head

    // Calculate the length of the linked list
    while (right !== null) {
        right = right.next
        len++
    }

    // Move to the start of the second half of the list
    len = Math.floor(len / 2)
    right = head
    for (let i = 0; i < len; i++) {
        right = right.next
    }

    // Reverse the right half of the list
    let prev = null
    while (right !== null) {
        let next = right.next
        right.next = prev
        prev = right
        right = next
    }

    // Compare the left half and the reversed right half
    for (let i = 0; i < len; i++) {
        if (prev !== null && head.val === prev.val) {
            head = head.next
            prev = prev.next
        } else {
            return false
        }
    }
    return true
};

export { isPalindrome }
```