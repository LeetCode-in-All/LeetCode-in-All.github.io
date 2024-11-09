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

```c
#include <stdio.h>
#include <stdlib.h>

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
// Global variable to store the maximum diameter
int diameter;

// Helper function to calculate the diameter of the binary tree
int diameterOfBinaryTreeUtil(struct TreeNode* root) {
    if (root == NULL) {
        return 0;
    }
    
    // Calculate left and right path lengths
    int leftLength = root->left ? 1 + diameterOfBinaryTreeUtil(root->left) : 0;
    int rightLength = root->right ? 1 + diameterOfBinaryTreeUtil(root->right) : 0;
    
    // Update the diameter if the path through this node is larger
    if (leftLength + rightLength > diameter) {
        diameter = leftLength + rightLength;
    }
    
    // Return the maximum path length from this node
    return leftLength > rightLength ? leftLength : rightLength;
}

// Main function to find the diameter of the binary tree
int diameterOfBinaryTree(struct TreeNode* root) {
    diameter = 0; // Initialize diameter to 0
    diameterOfBinaryTreeUtil(root); // Calculate diameter using the utility function
    return diameter;
}
```