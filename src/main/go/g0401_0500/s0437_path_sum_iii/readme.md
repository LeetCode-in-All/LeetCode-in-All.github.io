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

```golang
type TreeNode struct {
	Val   int
	Left  *TreeNode
	Right *TreeNode
}

/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func pathSum(root *TreeNode, targetSum int) int {
	mp := make(map[int]int)
	mp[0] = 1

	return solve(root, 0, targetSum, mp)
}

func solve(root *TreeNode, currSum, target int, mp map[int]int) int {
	if root == nil {
		return 0
	}

	currSum += root.Val
	res := 0
	if val, ok := mp[currSum-target]; ok {
		res = val
	}
	if val, ok := mp[currSum]; ok {
		mp[currSum] = val + 1
	} else {
		mp[currSum] = 1
	}

	res += solve(root.Left, currSum, target, mp) + solve(root.Right, currSum, target, mp)
	if val, ok := mp[currSum]; ok {
		mp[currSum] = val - 1
	}

	return res
}
```