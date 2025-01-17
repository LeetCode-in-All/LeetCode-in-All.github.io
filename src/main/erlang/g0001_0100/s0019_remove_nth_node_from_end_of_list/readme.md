[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 19\. Remove Nth Node From End of List

Medium

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

**Input:** head = [1,2,3,4,5], n = 2

**Output:** [1,2,3,5]

**Example 2:**

**Input:** head = [1], n = 1

**Output:** []

**Example 3:**

**Input:** head = [1,2], n = 1

**Output:** [1]

**Constraints:**

*   The number of nodes in the list is `sz`.
*   `1 <= sz <= 30`
*   `0 <= Node.val <= 100`
*   `1 <= n <= sz`

**Follow up:** Could you do this in one pass?

## Solution

```erlang
%% Definition for singly-linked list.
%%
%% -record(list_node, {val = 0 :: integer(),
%%                     next = null :: 'null' | #list_node{}}).

%% Remove nth node from end of list
-spec remove_nth_from_end(Head :: #list_node{} | null, N :: integer()) -> #list_node{} | null.
remove_nth_from_end(Head, N) ->
    Dummy = #list_node{val = 0, next = Head},
    {_, Result} = remove_nth(Dummy, N),
    Result#list_node.next.

%% Helper function that returns {RemainingCount, Node}
-spec remove_nth(Node :: #list_node{} | null, N :: integer()) -> {integer(), #list_node{}}.
remove_nth(Node, N) when Node#list_node.next =:= null ->
    {N, Node};
remove_nth(Node, N) ->
    {RemainingCount, UpdatedNext} = remove_nth(Node#list_node.next, N),
    NewCount = RemainingCount - 1,
    
    case NewCount of
        0 -> 
            % Remove the next node by skipping it
            NewNode = Node#list_node{next = UpdatedNext#list_node.next},
            {NewCount, NewNode};
        _ -> 
            % Keep the next node as is
            NewNode = Node#list_node{next = UpdatedNext},
            {NewCount, NewNode}
    end.
```