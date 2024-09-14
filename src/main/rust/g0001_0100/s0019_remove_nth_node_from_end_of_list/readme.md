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
    pub fn remove_nth_from_end(head: Option<Box<ListNode>>, n: i32) -> Option<Box<ListNode>> {
        // Use a naive solution
        // Get the length of the list
        // Traverse again up to target - 1, remove target and point next to the next item
        let mut length: i32 = 0;
        let mut node: &Option<Box<ListNode>> = &head;
        while let Some(node_val) = node {
            length += 1;
            node = &node_val.next;
        }

        // Create a new list to contain the result with node removed from it
        let mut result = Some(Box::new(ListNode::new(0)));
        let mut current = result.as_mut();
        let mut node = &head;
        let mut x: i32 = 1;

        while let Some(node_val) = node {
            if (length - x + 1) != n {
                current.as_mut().unwrap().next = Some(Box::new(ListNode::new(node_val.val)));
                current = current.unwrap().next.as_mut();
            }
            x += 1;
            node = &node_val.next;
        }

        result.unwrap().next
    }
}
```