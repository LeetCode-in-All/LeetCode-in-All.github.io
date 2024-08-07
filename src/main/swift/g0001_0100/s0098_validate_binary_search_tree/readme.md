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

To solve the "Validate Binary Search Tree" problem in Swift with the Solution class, follow these steps:

1. Define a method `isValidBST` in the `Solution` class that takes the root of a binary tree as input and returns true if the tree is a valid binary search tree (BST), and false otherwise.
2. Implement a recursive approach to validate if the given binary tree is a valid BST:
   - Define a helper method `isValidBSTHelper` that takes the root node, a lower bound, and an upper bound as input parameters.
   - In the `isValidBSTHelper` method, recursively traverse the binary tree nodes.
   - At each node, check if its value is within the specified bounds (lower bound and upper bound) for a valid BST.
   - If the node's value violates the BST property, return false.
   - Otherwise, recursively validate the left and right subtrees by updating the bounds accordingly.
   - If both the left and right subtrees are valid BSTs, return true.
3. Call the `isValidBSTHelper` method with the root node and appropriate initial bounds to start the validation process.

Here's the implementation of the `isValidBST` method in Swift:

```swift
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public var val: Int
 *     public var left: TreeNode?
 *     public var right: TreeNode?
 *     public init() { self.val = 0; self.left = nil; self.right = nil; }
 *     public init(_ val: Int) { self.val = val; self.left = nil; self.right = nil; }
 *     public init(_ val: Int, _ left: TreeNode?, _ right: TreeNode?) {
 *         self.val = val
 *         self.left = left
 *         self.right = right
 *     }
 * }
 */
class Solution {
    func isValidBST(_ root: TreeNode?) -> Bool {
        return solve(root, Int.min, Int.max)
    }

    private func solve(_ root: TreeNode?, _ left: Int, _ right: Int) -> Bool {
        guard let root = root else {
            return true
        }
        if root.val <= left || root.val >= right {
            return false
        }
        return solve(root.left, left, root.val) && solve(root.right, root.val, right)
    }
}
```

This implementation recursively validates whether the given binary tree is a valid BST in O(n) time complexity, where n is the number of nodes in the tree.