[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 24\. Swap Nodes in Pairs

Medium

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)

**Input:** head = [1,2,3,4]

**Output:** [2,1,4,3]

**Example 2:**

**Input:** head = []

**Output:** []

**Example 3:**

**Input:** head = [1]

**Output:** [1]

**Constraints:**

*   The number of nodes in the list is in the range `[0, 100]`.
*   `0 <= Node.val <= 100`

## Solution

```erlang
%% Definition for singly-linked list.
%%
%% -record(list_node, {val = 0 :: integer(),
%%                     next = null :: 'null' | #list_node{}}).

%% Swap every two adjacent nodes in a linked list
-spec swap_pairs(Head :: #list_node{} | null) -> #list_node{} | null.
swap_pairs(null) -> null;
swap_pairs(#list_node{next = null} = Head) -> Head;
swap_pairs(First = #list_node{next = Second}) ->
    NextPair = Second#list_node.next,
    % Connect second node to first
    Second#list_node{
        next = First#list_node{
            % Connect first node to result of swapping remaining pairs
            next = swap_pairs(NextPair)
        }
    }.
```