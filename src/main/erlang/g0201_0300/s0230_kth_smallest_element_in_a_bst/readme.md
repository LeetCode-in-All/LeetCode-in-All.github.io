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

```erlang
%% Definition for a binary tree node.
%%
%% -record(tree_node, {val = 0 :: integer(),
%%                     left = null  :: 'null' | #tree_node{},
%%                     right = null :: 'null' | #tree_node{}}).

% Main function to find kth smallest element
-spec kth_smallest(Root :: #tree_node{} | null, K :: integer()) -> integer().
kth_smallest(Root, K) ->
    {_, Value} = find_kth_smallest(Root, K, 0),
    Value.

% Helper function to traverse the tree and find kth smallest
-spec find_kth_smallest(Node :: #tree_node{} | null, K :: integer(), Count :: integer()) -> 
    {integer(), integer() | null}.
find_kth_smallest(null, _, Count) ->
    {Count, null};
find_kth_smallest(Node, K, Count) ->
    % Search left subtree
    {NewCount, LeftValue} = find_kth_smallest(Node#tree_node.left, K, Count),
    
    % If we found the value in left subtree, return it
    case LeftValue of
        null ->
            % Increment count for current node
            CurrentCount = NewCount + 1,
            
            % Check if current node is the kth smallest
            case CurrentCount =:= K of
                true ->
                    {CurrentCount, Node#tree_node.val};
                false ->
                    % Search right subtree
                    find_kth_smallest(Node#tree_node.right, K, CurrentCount)
            end;
        _ ->
            {NewCount, LeftValue}
    end.
```