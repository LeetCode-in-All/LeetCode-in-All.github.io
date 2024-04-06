[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 437\. Path Sum III

Medium

Given the `root` of a binary tree and an integer `targetSum`, return _the number of paths where the sum of the values along the path equals_ `targetSum`.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/04/09/pathsum3-1-tree.jpg)

**Input:** root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8

**Output:** 3

**Explanation:** The paths that sum to 8 are shown. 

**Example 2:**

**Input:** root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22

**Output:** 3 

**Constraints:**

*   The number of nodes in the tree is in the range `[0, 1000]`.
*   <code>-10<sup>9</sup> <= Node.val <= 10<sup>9</sup></code>
*   `-1000 <= targetSum <= 1000`

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
    private int count = 0;

    public int PathSum(TreeNode root, int targetSum) {
        if (root == null) {
            return 0;
        }
        Helper(root, targetSum, 0);
        PathSum(root.left, targetSum);
        PathSum(root.right, targetSum);
        return count;
    }

    public void Helper(TreeNode node, int targetSum, long currSum) {
        currSum += (long) node.val;
        if (targetSum == currSum) {
            count++;
        }
        if (node.left != null) {
            Helper(node.left, targetSum, currSum);
        }
        if (node.right != null) {
            Helper(node.right, targetSum, currSum);
        }
    }
}
```