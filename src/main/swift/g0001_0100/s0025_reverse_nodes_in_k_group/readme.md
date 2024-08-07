[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 25\. Reverse Nodes in k-Group

Hard

Given a linked list, reverse the nodes of a linked list _k_ at a time and return its modified list.

_k_ is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of _k_ then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

**Input:** head = [1,2,3,4,5], k = 2

**Output:** [2,1,4,3,5] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg)

**Input:** head = [1,2,3,4,5], k = 3

**Output:** [3,2,1,4,5] 

**Example 3:**

**Input:** head = [1,2,3,4,5], k = 1

**Output:** [1,2,3,4,5] 

**Example 4:**

**Input:** head = [1], k = 1

**Output:** [1] 

**Constraints:**

*   The number of nodes in the list is in the range `sz`.
*   `1 <= sz <= 5000`
*   `0 <= Node.val <= 1000`
*   `1 <= k <= sz`

**Follow-up:** Can you solve the problem in O(1) extra memory space?

To solve the "Reverse Nodes in k-Group" problem in Swift with a `Solution` class, we can reverse the nodes in groups of k using a recursive approach. Here are the steps:

1. Define a `Solution` class.
2. Define a method named `reverseKGroup` that takes the head of a linked list and an integer k as input and returns the head of the modified list.
3. Define a helper method named `reverse` that takes the head and tail of a sublist as input and reverses the sublist in place. This method returns the new head of the sublist.
4. Create a dummy ListNode object and set its `next` pointer to the head of the input list. This dummy node will serve as the new head of the modified list.
5. Initialize pointers `prev`, `curr`, `next`, and `tail`. Set `prev` and `tail` to the dummy node, and `curr` to the head of the input list.
6. Iterate through the list:
   - Move `curr` k steps forward. If it's not possible (i.e., there are less than k nodes left), break the loop.
   - Set `next` to the `next` pointer of `curr`.
   - Reverse the sublist from `curr` to `next` using the `reverse` method. Update `prev` and `tail` accordingly.
   - Move `prev` and `tail` k steps forward to the last node of the reversed sublist.
   - Move `curr` to `next`.
7. Return the `next` pointer of the dummy node, which points to the head of the modified list.

Here's the implementation:

```swift
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public var val: Int
 *     public var next: ListNode?
 *     public init() { self.val = 0; self.next = nil; }
 *     public init(_ val: Int) { self.val = val; self.next = nil; }
 *     public init(_ val: Int, _ next: ListNode?) { self.val = val; self.next = next; }
 * }
 */
public class Solution {
    public func reverseKGroup(_ head: ListNode?, _ k: Int) -> ListNode? {
        if head == nil || head?.next == nil || k == 1 {
            return head
        }
        
        var len = head
        var j = 0
        while j < k {
            if len == nil {
                return head
            }
            len = len?.next
            j += 1
        }
        
        var c = head
        var n: ListNode? = nil
        var prev: ListNode? = nil
        var i = 0
        
        while i < k {
            n = c?.next
            c?.next = prev
            prev = c
            c = n
            i += 1
        }
        
        head?.next = reverseKGroup(c, k)
        return prev
    }
}
```

This implementation provides a solution to the "Reverse Nodes in k-Group" problem in Swift without modifying the values in the list's nodes. It recursively reverses the nodes in groups of k.