[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 98\. Validate Binary Search Tree

Medium

Given the `root` of a binary tree, _determine if it is a valid binary search tree (BST)_.

A **valid BST** is defined as follows:

*   The left subtree of a node contains only nodes with keys **less than** the node's key.
*   The right subtree of a node contains only nodes with keys **greater than** the node's key.
*   Both the left and right subtrees must also be binary search trees.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

**Input:** root = [2,1,3]

**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

**Input:** root = [5,1,4,null,null,3,6]

**Output:** false

**Explanation:** The root node's value is 5 but its right child's value is 4.

**Constraints:**

*   The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.
*   <code>-2<sup>31</sup> <= Node.val <= 2<sup>31</sup> - 1</code>

## Solution

```rust
impl Solution {
    pub fn is_interleave(s1: String, s2: String, s3: String) -> bool {
        let mut state = vec![vec![None::<bool>; s2.len() + 1]; s1.len() + 1];
        is_interleave_0(&s1, &s2, &s3, &mut state)
    }
}

fn is_interleave_0(s1: &str, s2: &str, s3: &str, state: &mut Vec<Vec<Option<bool>>>) -> bool {
    if let Some(result) = state[s1.len()][s2.len()] {
        return result;
    }

    if s1.len() + s2.len() != s3.len() {
        return false;
    }

    if s1.is_empty() {
        return s2 == s3;
    }

    if s2.is_empty() {
        return s1 == s3;
    }

    let (head1, tail1) = s1.split_at(1);
    let (head2, tail2) = s2.split_at(1);
    let (head3, tail3) = s3.split_at(1);

    if head1 == head3 && is_interleave_0(tail1, s2, tail3, state) {
        state[s1.len()][s2.len()] = Some(true);
        return true;
    } else if head2 == head3 && is_interleave_0(s1, tail2, tail3, state) {
        state[s1.len()][s2.len()] = Some(true);
        return true;
    } else {
        state[s1.len()][s2.len()] = Some(false);
        return false;
    }
}
```