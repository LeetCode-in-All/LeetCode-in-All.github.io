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

```php
use leetcode\com_github_leetcode\TreeNode;

/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($val = 0, $left = null, $right = null) {
 *         $this->val = $val;
 *         $this->left = $left;
 *         $this->right = $right;
 *     }
 * }
 */
class Solution {
    private $j;
    private $map;

    function __construct() {
        $this->j = 0;
        $this->map = array();
    }

    function get($key) {
        return $this->map[$key];
    }

    private function answer($preorder, $inorder, $start, $end) {
        if ($start > $end || $this->j > count($preorder)) {
            return null;
        }
        $value = $preorder[$this->j++];
        $index = $this->get($value);
        $node = new TreeNode($value);
        $node->left = $this->answer($preorder, $inorder, $start, $index - 1);
        $node->right = $this->answer($preorder, $inorder, $index + 1, $end);
        return $node;
    }

    /**
     * @param Integer[] $preorder
     * @param Integer[] $inorder
     * @return TreeNode
     */
    function buildTree($preorder, $inorder) {
        $this->j = 0;
        for ($i = 0; $i < count($preorder); $i++) {
            $this->map[$inorder[$i]] = $i;
        }
        return $this->answer($preorder, $inorder, 0, count($preorder) - 1);
    }
}
```