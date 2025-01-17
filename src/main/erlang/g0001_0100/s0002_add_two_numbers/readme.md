[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 2\. Add Two Numbers

Medium

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

**Input:** l1 = [2,4,3], l2 = [5,6,4]

**Output:** [7,0,8]

**Explanation:** 342 + 465 = 807. 

**Example 2:**

**Input:** l1 = [0], l2 = [0]

**Output:** [0] 

**Example 3:**

**Input:** l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]

**Output:** [8,9,9,9,0,0,0,1] 

**Constraints:**

*   The number of nodes in each linked list is in the range `[1, 100]`.
*   `0 <= Node.val <= 9`
*   It is guaranteed that the list represents a number that does not have leading zeros.

## Solution

```erlang
%% Definition for singly-linked list.
%%
%% -record(list_node, {val = 0 :: integer(),
%%                     next = null :: 'null' | #list_node{}}).

-spec add_two_numbers(L1 :: #list_node{} | null, L2 :: #list_node{} | null) -> #list_node{} | null.
add_two_numbers(L1, L2) ->
    {Result, _} = add_two_numbers(L1, L2, 0),
    Result.

-spec add_two_numbers(L1 :: #list_node{} | null, L2 :: #list_node{} | null, Carry :: integer()) -> {#list_node{} | null, integer()}.
add_two_numbers(null, null, 0) -> 
    {null, 0};
add_two_numbers(L1, L2, Carry) ->
    X = if L1 =/= null -> L1#list_node.val; true -> 0 end,
    Y = if L2 =/= null -> L2#list_node.val; true -> 0 end,
    Sum = Carry + X + Y,
    NewCarry = Sum div 10,
    NewNode = #list_node{val = Sum rem 10},
    {Next1, _} = if L1 =/= null -> {L1#list_node.next, 0}; true -> {null, 0} end,
    {Next2, _} = if L2 =/= null -> {L2#list_node.next, 0}; true -> {null, 0} end,
    {NextResult, _} = add_two_numbers(Next1, Next2, NewCarry),
    {NewNode#list_node{next = NextResult}, NewCarry}.
```