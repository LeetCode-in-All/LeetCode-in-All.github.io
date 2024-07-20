[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 543\. Diameter of Binary Tree

Easy

Given the `root` of a binary tree, return _the length of the **diameter** of the tree_.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)

**Input:** root = [1,2,3,4,5]

**Output:** 3

**Explanation:** 3 is the length of the path [4,2,1,3] or [5,2,1,3]. 

**Example 2:**

**Input:** root = [1,2]

**Output:** 1 

**Constraints:**

*   The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.
*   `-100 <= Node.val <= 100`

## Solution

```csharp
using LeetCodeNet.Com_github_leetcode;

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    private int diameter;

    public int DiameterOfBinaryTree(TreeNode root) {
        diameter = 0;
        DiameterOfBinaryTreeUtil(root);
        return diameter;
    }

    private int DiameterOfBinaryTreeUtil(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftLength = root.left != null ? 1 + DiameterOfBinaryTreeUtil(root.left) : 0;
        int rightLength = root.right != null ? 1 + DiameterOfBinaryTreeUtil(root.right) : 0;
        diameter = Math.Max(diameter, leftLength + rightLength);
        return Math.Max(leftLength, rightLength);
    }
}
```