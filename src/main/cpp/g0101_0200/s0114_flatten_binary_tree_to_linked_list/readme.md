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

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    void flatten(TreeNode* root) {
        if (root != nullptr) {
            findTail(root);
        }
    }

private:
    TreeNode* findTail(TreeNode* root) {
        TreeNode* left = root->left;
        TreeNode* right = root->right;
        TreeNode* tail;

        // Find the tail of left subtree, tail means the most left leaf
        if (left != nullptr) {
            tail = findTail(left);
            // Stitch the right subtree below the tail
            root->left = nullptr;
            root->right = left;
            tail->right = right;
        } else {
            tail = root;
        }

        // Find tail of the right subtree
        if (tail->right == nullptr) {
            return tail;
        } else {
            return findTail(tail->right);
        }
    }
};
```