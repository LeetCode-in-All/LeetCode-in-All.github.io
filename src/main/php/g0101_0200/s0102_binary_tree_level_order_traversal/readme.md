[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 102\. Binary Tree Level Order Traversal

Medium

Given the `root` of a binary tree, return _the level order traversal of its nodes' values_. (i.e., from left to right, level by level).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = [3,9,20,null,null,15,7]

**Output:** [[3],[9,20],[15,7]] 

**Example 2:**

**Input:** root = [1]

**Output:** [[1]] 

**Example 3:**

**Input:** root = []

**Output:** [] 

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 2000]`.
*   `-1000 <= Node.val <= 1000`

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
     * @return Integer[][]
     */
    function levelOrder($root) {
        $result = array();
        if ($root == null) {
            return $result;
        }
        $queue = new \SplQueue();
        $queue->enqueue($root);
        $queue->enqueue(null);
        $level = array();
        while (!$queue->isEmpty()) {
            $root = $queue->dequeue();
            while (!$queue->isEmpty() && $root != null) {
                array_push($level, $root->val);
                if ($root->left != null) {
                    $queue->enqueue($root->left);
                }
                if ($root->right != null) {
                    $queue->enqueue($root->right);
                }
                $root = $queue->dequeue();
            }
            array_push($result, $level);
            $level = array();
            if (!$queue->isEmpty()) {
                $queue->enqueue(null);
            }
        }
        return $result;
    }
}
```