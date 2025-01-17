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

```erlang
%% Definition for a binary tree node.
%%
%% -record(tree_node, {val = 0 :: integer(),
%%                     left = null  :: 'null' | #tree_node{},
%%                     right = null :: 'null' | #tree_node{}}).

-spec max_path_sum(Root :: #tree_node{} | null) -> integer().
max_path_sum(#tree_node{val = Val, left = null, right = null}) ->
    Val;
max_path_sum(Root) ->
    element(2, max_path(Root, -1001)).

-spec max_path(Node :: #tree_node{} | null, Max :: integer()) -> {integer(), integer()}.
max_path(null, Max) ->
    {0, Max};
max_path(#tree_node{val = Val, left = Left, right = Right}, Max) ->
    {LVal, LMax} = max_path(Left, Max),
    {RVal, RMax} = max_path(Right, Max),
    LocalMax = lists:max([LVal + Val, RVal + Val, Val]),
    GlobalMax = lists:max([Max, Val, Val + LVal, Val + RVal, Val + LVal + RVal, LMax, RMax]),
    {LocalMax, GlobalMax}.
```