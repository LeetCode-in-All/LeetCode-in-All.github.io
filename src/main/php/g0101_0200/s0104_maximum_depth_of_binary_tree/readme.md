[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 104\. Maximum Depth of Binary Tree

Easy

Given the `root` of a binary tree, return _its maximum depth_.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

**Input:** root = [3,9,20,null,null,15,7]

**Output:** 3 

**Example 2:**

**Input:** root = [1,null,2]

**Output:** 2 

**Example 3:**

**Input:** root = []

**Output:** 0 

**Example 4:**

**Input:** root = [0]

**Output:** 1 

**Constraints:**

*   The number of nodes in the tree is in the range <code>[0, 10<sup>4</sup>]</code>.
*   `-100 <= Node.val <= 100`

## Solution

```php
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
    /**
     * @param TreeNode $root
     * @return Integer
     */
    function maxDepth($root) {
        return $this->findDepth($root, 0);
    }

    private function findDepth($node, $currentDepth) {
        if ($node == null) {
            return 0;
        }
        $currentDepth++;
        return 1
            + max($this->findDepth($node->left, $currentDepth), $this->findDepth($node->right, $currentDepth));
    }
}
```