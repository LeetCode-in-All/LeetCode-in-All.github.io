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

```scala
import com_github_leetcode.TreeNode
import scala.collection.mutable.{ListBuffer, Queue}

/*
 * Definition for a binary tree node.
 * class TreeNode(_value: Int = 0, _left: TreeNode = null, _right: TreeNode = null) {
 *   var value: Int = _value
 *   var left: TreeNode = _left
 *   var right: TreeNode = _right
 * }
 */
object Solution {
    def levelOrder(root: TreeNode): List[List[Int]] = {
        val result = ListBuffer[List[Int]]()
        if (root == null) {
            return result.toList
        }
        val queue = Queue[TreeNode]()
        queue.enqueue(root)
        queue.enqueue(null)
        val level = ListBuffer[Int]()

        while (queue.nonEmpty) {
            val current = queue.dequeue()
            if (current != null) {
                level += current.value
                if (current.left != null) {
                    queue.enqueue(current.left)
                }
                if (current.right != null) {
                    queue.enqueue(current.right)
                }
            } else if (level.nonEmpty) {
                result += level.toList
                level.clear()
                queue.enqueue(null)
            }
        }

        result.toList
    }
}
```