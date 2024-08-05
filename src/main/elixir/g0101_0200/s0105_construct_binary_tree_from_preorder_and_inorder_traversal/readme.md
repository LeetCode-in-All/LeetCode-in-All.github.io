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
  @spec build_tree(preorder :: [integer], inorder :: [integer]) :: TreeNode.t() | nil
  def build_tree([], []), do: nil
  def build_tree(preorder, inorder) do
    [head | preorder] = preorder

    {left_inorder, [_ | right_inorder]} =
      inorder
      |> Enum.split_while(&(&1 != head))

    {left_preorder, right_preorder} = take_n_drop(preorder, length(left_inorder))

    %TreeNode{
      val: head,
      left: build_tree(left_preorder, left_inorder),
      right: build_tree(right_preorder, right_inorder)
    }
  end

  def take_n_drop(list, n, acc \\ [])

  def take_n_drop(list, 0, acc) do
    {acc |> Enum.reverse(), list}
  end

  def take_n_drop([head | tail], n, acc) do
    take_n_drop(tail, n - 1, [head | acc])
  end
end
```