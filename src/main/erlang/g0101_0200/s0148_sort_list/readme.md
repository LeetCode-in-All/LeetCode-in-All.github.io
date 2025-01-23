[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 148\. Sort List

Medium

Given the `head` of a linked list, return _the list after sorting it in **ascending order**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg)

**Input:** head = [4,2,1,3]

**Output:** [1,2,3,4]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg)

**Input:** head = [-1,5,3,4,0]

**Output:** [-1,0,3,4,5]

**Example 3:**

**Input:** head = []

**Output:** []

**Constraints:**

*   The number of nodes in the list is in the range <code>[0, 5 * 10<sup>4</sup>]</code>.
*   <code>-10<sup>5</sup> <= Node.val <= 10<sup>5</sup></code>

**Follow up:** Can you sort the linked list in `O(n logn)` time and `O(1)` memory (i.e. constant space)?

## Solution

```erlang
%% Definition for singly-linked list.
%%
%% -record(list_node, {val = 0 :: integer(),
%%                     next = null :: 'null' | #list_node{}}).

%% @spec sort_list(Head :: #list_node{} | null) -> #list_node{} | null.
-spec sort_list(Head :: #list_node{} | null) -> #list_node{} | null.
sort_list(Head) ->
    List = node_to_list(Head, []),
    SortedList = lists:sort(fun(X, Y) -> X > Y end, List),
    list_to_node(SortedList, null).

%% Converts a linked list to an Erlang list.
-spec node_to_list(Node :: #list_node{} | null, Acc :: [integer()]) -> [integer()].
node_to_list(null, Acc) ->
    Acc;
node_to_list(#list_node{val = Val, next = Next}, Acc) ->
    node_to_list(Next, [Val | Acc]).

%% Converts an Erlang list to a linked list.
-spec list_to_node(List :: [integer()], Node :: #list_node{} | null) -> #list_node{} | null.
list_to_node([], Node) ->
    Node;
list_to_node([H | T], Node) ->
    list_to_node(T, #list_node{val = H, next = Node}).
```