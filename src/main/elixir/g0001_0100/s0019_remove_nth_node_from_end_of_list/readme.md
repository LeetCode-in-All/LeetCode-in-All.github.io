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

```elixir
# Definition for singly-linked list.
#
# defmodule ListNode do
#   @type t :: %__MODULE__{
#           val: integer,
#           next: ListNode.t() | nil
#         }
#   defstruct val: 0, next: nil
# end

defmodule Solution do
  @spec remove_nth_from_end(head :: ListNode.t | nil, n :: integer) :: ListNode.t | nil
  def remove_nth_from_end(%ListNode{next: nil}, 1), do: nil

  def remove_nth_from_end(list_node, 1) do
    list_node
    |> node_list_to_array()
    |> Enum.slice(1..-1)
    |> array_to_list_node()
  end

  def remove_nth_from_end(%ListNode{} = head, n) do
    n = n - 1
    head = node_list_to_array(head)
    head = Enum.slice(head, 0..(n - 1)) |> Enum.concat(Enum.slice(head, (n + 1)..-1))
    array_to_list_node(head)
  end

  def node_list_to_array(list_node), do: node_list_to_array(list_node, [])
  def node_list_to_array(%ListNode{next: nil, val: elem}, array), do: [elem | array]

  def node_list_to_array(%ListNode{next: some, val: elem}, array) do
    node_list_to_array(some, [elem | array])
  end

  def array_to_list_node([h | t]) do
    array_to_list_node(t, %ListNode{next: nil, val: h})
  end

  def array_to_list_node([], last_node), do: last_node

  def array_to_list_node([h | t], last_node) do
    array_to_list_node(t, %ListNode{next: last_node, val: h})
  end
end
```