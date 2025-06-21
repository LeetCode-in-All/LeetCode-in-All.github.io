[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 230\. Kth Smallest Element in a BST

Medium

Given the `root` of a binary search tree, and an integer `k`, return _the_ <code>k<sup>th</sup></code> _smallest value (**1-indexed**) of all the values of the nodes in the tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg)

**Input:** root = [3,1,4,null,2], k = 1

**Output:** 1 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg)

**Input:** root = [5,3,6,2,4,null,null,1], k = 3

**Output:** 3 

**Constraints:**

*   The number of nodes in the tree is `n`.
*   <code>1 <= k <= n <= 10<sup>4</sup></code>
*   <code>0 <= Node.val <= 10<sup>4</sup></code>

**Follow up:** If the BST is modified often (i.e., we can do insert and delete operations) and you need to find the kth smallest frequently, how would you optimize?

## Solution

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */
function kthSmallest(root: TreeNode | null, k: number): number {
    let cur = root
    while (cur !== null) {
        if (cur.left !== null) {
            const left = cur.left
            cur.left = null
            let rightmost = left
            while (rightmost.right !== null) rightmost = rightmost.right
            rightmost.right = cur
            cur = left
        } else if (--k !== 0) {
            cur = cur.right
        } else {
            break
        }
    }
    return cur.val
}

export { kthSmallest }
```