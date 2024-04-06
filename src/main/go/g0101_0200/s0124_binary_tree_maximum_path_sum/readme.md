[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 124\. Binary Tree Maximum Path Sum

Hard

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return _the maximum **path sum** of any **non-empty** path_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg)

**Input:** root = [1,2,3]

**Output:** 6

**Explanation:** The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/13/exx2.jpg)

**Input:** root = [-10,9,20,null,null,15,7]

**Output:** 42

**Explanation:** The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.

**Constraints:**

*   The number of nodes in the tree is in the range <code>[1, 3 * 10<sup>4</sup>]</code>.
*   `-1000 <= Node.val <= 1000`

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
func deepest(root *TreeNode, ans *int) int {
	if root == nil {
		return 0
	}
	l := deepest(root.Left, ans)
	r := deepest(root.Right, ans)
	if l+root.Val > *ans {
		*ans = l + root.Val
	}
	if r+root.Val > *ans {
		*ans = r + root.Val
	}
	if l+r+root.Val > *ans {
		*ans = l + r + root.Val
	}
	if root.Val > *ans {
		*ans = root.Val
	}
	if l > r && l > 0 {
		return root.Val + l
	}
	if r > 0 {
		return root.Val + r
	}
	return root.Val
}

func maxPathSum(root *TreeNode) int {
	ans := -100000000
	deepest(root, &ans)
	return ans
}
```