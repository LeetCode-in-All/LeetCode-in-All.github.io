[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 98\. Validate Binary Search Tree

Medium

Given the `root` of a binary tree, _determine if it is a valid binary search tree (BST)_.

A **valid BST** is defined as follows:

*   The left subtree of a node contains only nodes with keys **less than** the node's key.
*   The right subtree of a node contains only nodes with keys **greater than** the node's key.
*   Both the left and right subtrees must also be binary search trees.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

**Input:** root = [2,1,3]

**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

**Input:** root = [5,1,4,null,null,3,6]

**Output:** false

**Explanation:** The root node's value is 5 but its right child's value is 4.

**Constraints:**

*   The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.
*   <code>-2<sup>31</sup> <= Node.val <= 2<sup>31</sup> - 1</code>

## Solution

```elixir
# Definition for a binary tree node.
#
# defmodule TreeNode do
#   @type t :: %__MODULE__{
#           val: integer,
#           left: TreeNode.t() | nil,
#           right: TreeNode.t() | nil
#         }
#   defstruct val: 0, left: nil, right: nil
# end

defmodule Solution do
  @spec is_valid_bst(root :: TreeNode.t() | nil) :: boolean
  def is_valid_bst(root) do
    root |> inorder_check() |> is_list()
  end

  @spec inorder_check(root :: TreeNode.t() | nil) :: [integer] | :invalid
  def inorder_check(root) do
    inorder_check(root, [])
  end

  def inorder_check(nil, acc), do: acc

  def inorder_check(root, acc) do
    # root comes in between in inorder traversal
    case inorder_check(root.left, acc) do
      [x | _] = acc ->
        if x >= root.val do
          :invalid
        else
          acc = [root.val | acc]
          inorder_check(root.right, acc)
        end

      [] ->
        acc = [root.val | acc]
        inorder_check(root.right, acc)

      _ ->
        :invalid
    end
  end
end
```