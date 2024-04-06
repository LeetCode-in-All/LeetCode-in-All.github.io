[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 234\. Palindrome Linked List

Easy

Given the `head` of a singly linked list, return `true` if it is a palindrome.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

**Input:** head = [1,2,2,1]

**Output:** true 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

**Input:** head = [1,2]

**Output:** false 

**Constraints:**

*   The number of nodes in the list is in the range <code>[1, 10<sup>5</sup>]</code>.
*   `0 <= Node.val <= 9`

**Follow up:** Could you do it in `O(n)` time and `O(1)` space?

## Solution

```ruby
require_relative '../../com_github_leetcode/list_node'

# Definition for singly-linked list.
# class ListNode
#     attr_accessor :val, :next
#     def initialize(val = 0, _next = nil)
#         @val = val
#         @next = _next
#     end
# end
# @param {ListNode} head
# @return {Boolean}
def is_palindrome2(head)
    # find mid, reverse second half of list, compare the nodes of 'two' lists
    slow = fast = head
    while fast && fast.next do 
        slow = slow.next
        fast = fast.next.next
    end
    mid_head = slow

    curr = mid_head
    prev = nil
    while curr do 
        next_node = curr.next 
        curr.next = prev
        prev = curr
        curr = next_node
    end
    prev

    curr = head
    mid_curr= prev
    while curr && mid_curr do 
        if curr.val != mid_curr.val
            return false
        end
        
        curr = curr.next
        mid_curr = mid_curr.next
    end

    true
end
```