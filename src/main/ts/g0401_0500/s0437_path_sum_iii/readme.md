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

```typescript
function pathSum(root: TreeNode | null, targetSum: number): number {
    let count = 0
    let map = new Map<number, number>()

    function dfs(node: TreeNode | null, currentSum: number): void {
        if (!node) {
            return
        }
        currentSum += node.val
        if (currentSum === targetSum) {
            count++
        }
        count += map.get(currentSum - targetSum) ?? 0
        map.set(currentSum, map.get(currentSum) + 1 || 1)
        dfs(node?.left, currentSum)
        dfs(node?.right, currentSum)
        //remove from hashmap
        map.set(currentSum, map.get(currentSum) - 1)
        if (map.get(currentSum) === 0) {
            map.delete(currentSum)
        }
    }

    dfs(root, 0)
    return count
}

export { pathSum }
```