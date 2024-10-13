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

```dart
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *   int val;
 *   TreeNode? left;
 *   TreeNode? right;
 *   TreeNode([this.val = 0, this.left, this.right]);
 * }
 */
class Solution {
  int _j = 0;
  Map<int, int> _map = {};

  int get(int key) {
    return _map[key]!;
  }

  TreeNode? answer(List<int> preorder, List<int> inorder, int start, int end) {
    if (start > end || _j >= preorder.length) {
      return null;
    }
    int value = preorder[_j++];
    int index = get(value);
    TreeNode node = TreeNode(value);
    node.left = answer(preorder, inorder, start, index - 1);
    node.right = answer(preorder, inorder, index + 1, end);
    return node;
  }

  TreeNode? buildTree(List<int> preorder, List<int> inorder) {
    _j = 0;
    for (int i = 0; i < inorder.length; i++) {
      _map[inorder[i]] = i;
    }
    return answer(preorder, inorder, 0, preorder.length - 1);
  }
}
```