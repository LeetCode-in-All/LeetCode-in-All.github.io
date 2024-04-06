[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 114\. Flatten Binary Tree to Linked List

Medium

Given the `root` of a binary tree, flatten the tree into a "linked list":

*   The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
*   The "linked list" should be in the same order as a [**pre-order** **traversal**](https://en.wikipedia.org/wiki/Tree_traversal#Pre-order,_NLR) of the binary tree.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg)

**Input:** root = [1,2,5,3,4,null,6]

**Output:** [1,null,2,null,3,null,4,null,5,null,6] 

**Example 2:**

**Input:** root = []

**Output:** [] 

**Example 3:**

**Input:** root = [0]

**Output:** [0] 

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 2000]`.
*   `-100 <= Node.val <= 100`

**Follow up:** Can you flatten the tree in-place (with `O(1)` extra space)?

## Solution

```scala
import com_github_leetcode.TreeNode

/*
 * Definition for a binary tree node.
 * class TreeNode(_value: Int = 0, _left: TreeNode = null, _right: TreeNode = null) {
 *   var value: Int = _value
 *   var left: TreeNode = _left
 *   var right: TreeNode = _right
 * }
 */
object Solution {
    def flatten(root: TreeNode): Unit = {
        if (root != null) {
            modifyToRight(root)
        }
    }

    private def modifyToRight(root: TreeNode): TreeNode = {
        if (root.left == null && root.right == null) {
            root
        } else if (root.left == null) {
            root.right = modifyToRight(root.right)
            root
        } else if (root.right == null) {
            val left = modifyToRight(root.left)
            root.left = null
            root.right = left
            root
        } else {
            val left = modifyToRight(root.left)
            val right = modifyToRight(root.right)
            traverseAndAppend(left, right)
            root.right = left
            root.left = null
            root
        }
    }

    private def traverseAndAppend(root: TreeNode, right: TreeNode): Unit = {
        if (root.right != null) {
            traverseAndAppend(root.right, right)
        } else {
            root.right = right
        }
    }
}
```