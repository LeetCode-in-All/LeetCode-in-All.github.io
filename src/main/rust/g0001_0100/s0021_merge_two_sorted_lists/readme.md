[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 21\. Merge Two Sorted Lists

Easy

Merge two sorted linked lists and return it as a **sorted** list. The list should be made by splicing together the nodes of the first two lists.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

**Input:** l1 = [1,2,4], l2 = [1,3,4]

**Output:** [1,1,2,3,4,4]

**Example 2:**

**Input:** l1 = [], l2 = []

**Output:** []

**Example 3:**

**Input:** l1 = [], l2 = [0]

**Output:** [0]

**Constraints:**

*   The number of nodes in both lists is in the range `[0, 50]`.
*   `-100 <= Node.val <= 100`
*   Both `l1` and `l2` are sorted in **non-decreasing** order.

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
    pub fn merge_two_lists(
        mut l1: Option<Box<ListNode>>,
        mut l2: Option<Box<ListNode>>,
    ) -> Option<Box<ListNode>> {
        let mut dummy = Some(Box::new(ListNode::new(-1)));
        let mut current = &mut dummy;

        while l1.is_some() || l2.is_some() {
            if let (Some(ref l1_node), Some(ref l2_node)) = (&l1, &l2) {
                if l1_node.val <= l2_node.val {
                    current.as_mut().unwrap().next = l1.take();
                    l1 = current.as_mut().unwrap().next.as_mut().unwrap().next.take();
                } else {
                    current.as_mut().unwrap().next = l2.take();
                    l2 = current.as_mut().unwrap().next.as_mut().unwrap().next.take();
                }
            } else if l1.is_some() {
                current.as_mut().unwrap().next = l1.take();
            } else {
                current.as_mut().unwrap().next = l2.take();
            }
            current = &mut current.as_mut().unwrap().next;
        }

        dummy.unwrap().next
    }
}
```