[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 21\. Merge Two Sorted Lists

Easy

Merge two sorted linked lists and return it as a **sorted** list. The list should be made by splicing together the nodes of the first two lists.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

**Input:** l1 = [1,2,4], l2 = [1,3,4]

**Output:** [1,1,2,3,4,4]

**Example 2:**

**Input:** l1 = [], l2 = []

**Output:** []

**Example 3:**

**Input:** l1 = [], l2 = [0]

**Output:** [0]

**Constraints:**

*   The number of nodes in both lists is in the range `[0, 50]`.
*   `-100 <= Node.val <= 100`
*   Both `l1` and `l2` are sorted in **non-decreasing** order.

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
  @spec merge_two_lists(list1 :: ListNode.t() | nil, list2 :: ListNode.t() | nil) :: ListNode.t() | nil
  def merge_two_lists(nil, nil), do: nil
  def merge_two_lists(list1, nil), do: list1
  def merge_two_lists(nil, list2), do: list2

  def merge_two_lists(%ListNode{val: val1, next: next1} = list1, %ListNode{val: val2, next: next2} = list2) do
    if val1 <= val2 do
      %ListNode{val: val1, next: merge_two_lists(next1, list2)}
    else
      %ListNode{val: val2, next: merge_two_lists(list1, next2)}
    end
  end
end
```