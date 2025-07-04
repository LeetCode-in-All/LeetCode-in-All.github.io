[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 25\. Reverse Nodes in k-Group

Hard

Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return _the modified list_.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

**Input:** head = [1,2,3,4,5], k = 2

**Output:** [2,1,4,3,5] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg)

**Input:** head = [1,2,3,4,5], k = 3

**Output:** [3,2,1,4,5] 

**Constraints:**

*   The number of nodes in the list is `n`.
*   `1 <= k <= n <= 5000`
*   `0 <= Node.val <= 1000`

**Follow-up:** Can you solve the problem in `O(1)` extra memory space?

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
func reverseKGroup(head *ListNode, k int) *ListNode {
	if head == nil || head.Next == nil || k == 1 {
		return head
	}
	j := 0
	len := head
	// Loop to check the length of the linked list. If the list is less than k, return as it is.
	for j < k {
		if len == nil {
			return head
		}
		len = len.Next
		j++
	}
	// Apply reverse linked list logic.
	c := head
	var n *ListNode
	var prev *ListNode
	i := 0
	// Traverse the while loop for k times to reverse the nodes in k groups.
	for i != k {
		n = c.Next
		c.Next = prev
		prev = c
		c = n
		i++
	}
	// head points to the first node of the k group, which now points to the next k group.
	// Recurse for the remaining linked list.
	head.Next = reverseKGroup(n, k)
	return prev
}
```