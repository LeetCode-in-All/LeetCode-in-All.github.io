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

```ruby
# Definition for singly-linked list.
# class ListNode
#     attr_accessor :val, :next
#     def initialize(val = 0, _next = nil)
#         @val = val
#         @next = _next
#     end
# end
# @param {ListNode} head
# @return {ListNode}
def swap_pairs(head)
  return nil if head.nil?
  len = get_length(head)
  reverse_pairs(head, len)
end

def get_length(curr)
  cnt = 0
  while curr
    cnt += 1
    curr = curr.next
  end
  cnt
end

# Recursive function to reverse in groups
def reverse_pairs(head, len)
  # base case
  return head if len < 2

  curr = head
  prev = nil
  next_node = nil

  2.times do
    # reverse linked list code
    next_node = curr.next
    curr.next = prev
    prev = curr
    curr = next_node
  end

  head.next = reverse_pairs(curr, len - 2)
  prev
end
```