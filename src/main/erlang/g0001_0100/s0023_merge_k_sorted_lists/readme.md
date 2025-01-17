[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 23\. Merge k Sorted Lists

Hard

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

_Merge all the linked-lists into one sorted linked-list and return it._

**Example 1:**

**Input:** lists = \[\[1,4,5],[1,3,4],[2,6]]

**Output:** [1,1,2,3,4,4,5,6]

**Explanation:** The linked-lists are: [ 1->4->5, 1->3->4, 2->6 ] merging them into one sorted list: 1->1->2->3->4->4->5->6

**Example 2:**

**Input:** lists = []

**Output:** []

**Example 3:**

**Input:** lists = \[\[]]

**Output:** []

**Constraints:**

*   `k == lists.length`
*   `0 <= k <= 10^4`
*   `0 <= lists[i].length <= 500`
*   `-10^4 <= lists[i][j] <= 10^4`
*   `lists[i]` is sorted in **ascending order**.
*   The sum of `lists[i].length` won't exceed `10^4`.

## Solution

```erlang
%% Definition for singly-linked list.
%%
%% -record(list_node, {val = 0 :: integer(),
%%                     next = null :: 'null' | #list_node{}}).

%% Merge k sorted linked lists
-spec merge_k_lists(Lists :: [#list_node{} | null]) -> #list_node{} | null.
merge_k_lists([]) ->
    null;
merge_k_lists(Lists) ->
    merge_k_lists(Lists, 0, length(Lists)).

%% Divide and conquer helper function
-spec merge_k_lists(Lists :: [#list_node{} | null], Left :: integer(), Right :: integer()) -> #list_node{} | null.
merge_k_lists(Lists, Left, Right) when Right > Left + 1 ->
    Mid = (Left + Right) div 2,
    LeftList = merge_k_lists(Lists, Left, Mid),
    RightList = merge_k_lists(Lists, Mid, Right),
    merge_two_lists(LeftList, RightList);
merge_k_lists(Lists, Left, _Right) ->
    lists:nth(Left + 1, Lists).

%% Merge two sorted lists
-spec merge_two_lists(Left :: #list_node{} | null, Right :: #list_node{} | null) -> #list_node{} | null.
merge_two_lists(null, Right) ->
    Right;
merge_two_lists(Left, null) ->
    Left;
merge_two_lists(Left = #list_node{val = LeftVal}, Right = #list_node{val = RightVal}) ->
    case LeftVal =< RightVal of
        true ->
            Left#list_node{next = merge_two_lists(Left#list_node.next, Right)};
        false ->
            Right#list_node{next = merge_two_lists(Left, Right#list_node.next)}
    end.
```