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
    pub fn is_palindrome(head: Option<Box<ListNode>>) -> bool {
        let mut ref_node = &head;
        let mut len = 0;

        while let Some(ref node) = &ref_node {
            ref_node = &node.next;
            len += 1;
        }

        ref_node = &head;
        let mut i = 0;
        let mut num = 0;
        let mut skip_num = if len % 2 == 1 { len / 2 + 1 } else { 0 };

        while let Some(node) = ref_node {
            ref_node = &node.next;

            if skip_num > 0 && skip_num - 1 == i {
                skip_num = 0;
                continue;
            }

            if i < len / 2 {
                num = num * 10 + node.val as usize;
            } else {
                num -= node.val as usize * 10_usize.pow(i - len / 2);
            }
            i += 1;
        }

        num == 0
    }
}
```