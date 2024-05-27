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

```cpp
#include <vector>
#include <unordered_map>

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
private:
    int j;
    std::unordered_map<int, int> map;

public:
    Solution() : j(0) {}

    TreeNode* buildTree(std::vector<int>& preorder, std::vector<int>& inorder) {
        map.clear();
        j = 0;
        for (int i = 0; i < inorder.size(); ++i) {
            map[inorder[i]] = i;
        }
        return answer(preorder, inorder, 0, preorder.size() - 1);
    }

private:
    TreeNode* answer(const std::vector<int>& preorder, const std::vector<int>& inorder, int start, int end) {
        if (start > end || j >= preorder.size()) {
            return nullptr;
        }
        int value = preorder[j++];
        int index = map[value];
        TreeNode* node = new TreeNode(value);
        node->left = answer(preorder, inorder, start, index - 1);
        node->right = answer(preorder, inorder, index + 1, end);
        return node;
    }
};
```