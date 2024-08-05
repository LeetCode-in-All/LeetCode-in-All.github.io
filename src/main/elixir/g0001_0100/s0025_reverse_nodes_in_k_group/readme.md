[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 25\. Reverse Nodes in k-Group

Hard

Given a linked list, reverse the nodes of a linked list _k_ at a time and return its modified list.

_k_ is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of _k_ then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

**Input:** head = [1,2,3,4,5], k = 2

**Output:** [2,1,4,3,5]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg)

**Input:** head = [1,2,3,4,5], k = 3

**Output:** [3,2,1,4,5]

**Example 3:**

**Input:** head = [1,2,3,4,5], k = 1

**Output:** [1,2,3,4,5]

**Example 4:**

**Input:** head = [1], k = 1

**Output:** [1]

**Constraints:**

*   The number of nodes in the list is in the range `sz`.
*   `1 <= sz <= 5000`
*   `0 <= Node.val <= 1000`
*   `1 <= k <= sz`

**Follow-up:** Can you solve the problem in O(1) extra memory space?

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
  @spec reverse_k_group(head :: ListNode.t() | nil, k :: integer) :: ListNode.t() | nil
  def reverse_k_group(head, k) do
    cond do
      # if length is less then k then do not change it
      length(0, head) < k -> head
      true -> head |> drop(k) |> reverse_k_group(k) |> reverse_list(head, k)
    end
  end

  def reverse_list(acc, _, 0), do: acc

  def reverse_list(acc, list, k) do
    reverse_list(%ListNode{list | next: acc}, list.next, k - 1)
  end

  def drop(nil, _), do: nil
  def drop(head, 0), do: head
  def drop(head, n), do: drop(head.next, n - 1)

  def length(acc, nil), do: acc
  def length(acc, head), do: length(acc + 1, head.next)

end
```