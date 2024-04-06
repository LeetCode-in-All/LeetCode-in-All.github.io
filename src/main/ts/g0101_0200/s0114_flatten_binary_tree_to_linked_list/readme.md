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

```typescript
import { TreeNode } from '../../com_github_leetcode/treenode'

/*
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

/**
 Do not return anything, modify root in-place instead.
 */
const flatten = (root: TreeNode | null): void => {
    if (root === null || (root.left === null && root.right === null)) {
        return
    }
    const vals: Array<number> = []
    const stack: Array<TreeNode> = []
    let next: TreeNode | null | undefined = root
    while (0 < stack.length || next != null) {
        while (next != null) {
            stack.push(next)
            vals.push(next.val)
            next = next.left
        }
        next = stack.pop()
        next = next?.right
    }
    let newHead: TreeNode | null = null
    let newTail: TreeNode | null = null
    for (let val of vals) {
        if (newHead == null) {
            newHead = new TreeNode(val)
            newTail = newHead
            continue
        }
        if (newTail != null) {
            newTail.right = new TreeNode(val)
            newTail = newTail.right
        }
    }
    if (newHead != null) {
        root.left = null
        root.val = newHead?.val
        root.right = newHead.right
    }
}

export { flatten }
```