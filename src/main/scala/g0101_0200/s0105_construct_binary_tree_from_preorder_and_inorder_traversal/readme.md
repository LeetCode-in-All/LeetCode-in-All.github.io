[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 105\. Construct Binary Tree from Preorder and Inorder Traversal

Medium

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return _the binary tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

**Input:** preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]

**Output:** [3,9,20,null,null,15,7] 

**Example 2:**

**Input:** preorder = [-1], inorder = [-1]

**Output:** [-1] 

**Constraints:**

*   `1 <= preorder.length <= 3000`
*   `inorder.length == preorder.length`
*   `-3000 <= preorder[i], inorder[i] <= 3000`
*   `preorder` and `inorder` consist of **unique** values.
*   Each value of `inorder` also appears in `preorder`.
*   `preorder` is **guaranteed** to be the preorder traversal of the tree.
*   `inorder` is **guaranteed** to be the inorder traversal of the tree.

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
    def buildTree(preorder: Array[Int], inorder: Array[Int]): TreeNode = {
        val map = inorder.zipWithIndex.toMap
        var j = 0

        def answer(start: Int, end: Int): TreeNode = {
            if (start > end || j >= preorder.length) {
                null
            } else {
                val value = preorder(j)
                j += 1
                val index = map(value)
                val node = new TreeNode(value)
                node.left = answer(start, index - 1)
                node.right = answer(index + 1, end)
                node
            }
        }

        answer(0, preorder.length - 1)
    }
}
```