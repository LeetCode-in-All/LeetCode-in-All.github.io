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

```ruby
# Definition for singly-linked list.
# class ListNode
#     attr_accessor :val, :next
#     def initialize(val = 0, _next = nil)
#         @val = val
#         @next = _next
#     end
# end
# @param {ListNode[]} lists
# @return {ListNode}
def merge_k_lists(lists)
  return nil if lists.empty?
  merge_k_lists_helper(lists, 0, lists.length)
end

def merge_k_lists_helper(lists, left_index, right_index)
  if right_index > left_index + 1
    mid = (left_index + right_index) / 2
    left = merge_k_lists_helper(lists, left_index, mid)
    right = merge_k_lists_helper(lists, mid, right_index)
    merge_two_lists(left, right)
  else
    lists[left_index]
  end
end

def merge_two_lists(left, right)
  return right if left.nil?
  return left if right.nil?

  res = nil
  if left.val <= right.val
    res = left
    left = left.next
  else
    res = right
    right = right.next
  end

  node = res
  while left || right
    if left.nil?
      node.next = right
      right = right.next
    elsif right.nil?
      node.next = left
      left = left.next
    else
      if left.val <= right.val
        node.next = left
        left = left.next
      else
        node.next = right
        right = right.next
      end
    end
    node = node.next
  end

  res
end
```