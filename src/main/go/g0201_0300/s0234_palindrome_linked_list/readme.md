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

```golang
type ListNode struct {
	Val  int
	Next *ListNode
}

/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func isPalindrome(head *ListNode) bool {
	// Calculate the length
	len := 0
	right := head
	for right != nil {
		right = right.Next
		len++
	}

	// Reverse the right half of the list
	len /= 2
	right = head
	for i := 0; i < len; i++ {
		right = right.Next
	}
	var prev *ListNode
	for right != nil {
		next := right.Next
		right.Next = prev
		prev = right
		right = next
	}

	// Compare left half and right half
	for i := 0; i < len; i++ {
		if prev != nil && head.Val == prev.Val {
			head = head.Next
			prev = prev.Next
		} else {
			return false
		}
	}
	return true
}
```