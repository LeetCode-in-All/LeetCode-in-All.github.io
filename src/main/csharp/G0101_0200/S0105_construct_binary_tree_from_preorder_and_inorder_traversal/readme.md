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
    private int j;
    private Dictionary<int, int> map = new Dictionary<int, int>();

    public int Get(int key) {
        return map[key];
    }

    private TreeNode Answer(int[] preorder, int[] inorder, int start, int end) {
        if (start > end || j > preorder.Length) {
            return null;
        }
        int value = preorder[j++];
        int index = Get(value);
        TreeNode node = new TreeNode(value);
        node.left = Answer(preorder, inorder, start, index - 1);
        node.right = Answer(preorder, inorder, index + 1, end);
        return node;
    }

    public TreeNode BuildTree(int[] preorder, int[] inorder) {
        j = 0;
        for (int i = 0; i < preorder.Length; i++) {
            map.Add(inorder[i], i);
        }
        return Answer(preorder, inorder, 0, preorder.Length - 1);
    }
}
```