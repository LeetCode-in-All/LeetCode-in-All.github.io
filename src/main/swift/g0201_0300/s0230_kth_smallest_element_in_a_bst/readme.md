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

```swift
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public var val: Int
 *     public var left: TreeNode?
 *     public var right: TreeNode?
 *     public init() { self.val = 0; self.left = nil; self.right = nil; }
 *     public init(_ val: Int) { self.val = val; self.left = nil; self.right = nil; }
 *     public init(_ val: Int, _ left: TreeNode?, _ right: TreeNode?) {
 *         self.val = val
 *         self.left = left
 *         self.right = right
 *     }
 * }
 */
class Solution {
    func kthSmallest(_ root: TreeNode?, _ k: Int) -> Int {
        var vals = [Int]()
        var minVal = Int.max
        var maxVal = Int.min
        traverse(root, &vals, &minVal, &maxVal)
        var countingArray = Array(repeating: -1, count: maxVal - minVal + 1)
        for val in vals { countingArray[val - minVal] = val }
        var i = 0
        for val in countingArray {
            guard val != -1 else { continue }
            i += 1
            if i == k { return val }
        }
        return -1
    }

    private func traverse(
        _ node: TreeNode?, 
        _ arr: inout [Int], 
        _ minVal: inout Int, 
        _ maxVal: inout Int
    ) {
        guard let node else { return }
        minVal = min(minVal, node.val)
        maxVal = max(maxVal, node.val)
        arr.append(node.val)
        traverse(node.left, &arr, &minVal, &maxVal)
        traverse(node.right, &arr, &minVal, &maxVal)
    }
}
```