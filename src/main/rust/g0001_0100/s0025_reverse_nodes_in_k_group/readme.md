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

## Solution

```rust
// Definition for singly-linked list.
// pub struct ListNode {
//   pub val: i32,
//   pub next: Option<Box<ListNode>>
// }
// 
// impl ListNode {
//   #[inline]
//   fn new(val: i32) -> Self {
//     ListNode {
//       next: None,
//       val
//     }
//   }
// }
impl Solution {
    pub fn reverse_k_group(mut head: Option<Box<ListNode>>, k: i32) -> Option<Box<ListNode>> {
        Solution::reverse(head, k)
    }
    pub fn reverse(mut head:Option<Box<ListNode>>, k: i32) -> Option<Box<ListNode>> {
        if head.is_none() {
            return None;
        }
        let mut new_head: Option<Box<ListNode>> = None;
        let mut i = 0;
        while let Some(mut head_val) = head.take() {
            head = head_val.next.take();
            head_val.next = new_head;
            new_head = Some(head_val);
            i += 1;
            if i == k {
                break;
            }
        }
        if i != k {
            // have to back out and return original list
            return Solution::reverse(new_head, i);
        }
        // we now have two lists:
        // head -> rest of list
        // new_head -> reversed list
        // i cannot figure out how in rust you do this in one pass, 
        // so we will go walk the list again to get the tail of new_head and make it head
        // 'append'
        head = Solution::reverse(head, k);
        let mut tailw = &mut new_head;
        if let Some(ref mut tail_val) = tailw {
            let mut tail = tail_val;
            while let Some(ref mut tail_next) = tail.next {
                tail = tail_next;
            }
            tail.next = head;
        }
        new_head
    }
}
```