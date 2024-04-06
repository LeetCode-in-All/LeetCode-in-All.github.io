[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 138\. Copy List with Random Pointer

Medium

A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.

Construct a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) of the list. The deep copy should consist of exactly `n` **brand new** nodes, where each new node has its value set to the value of its corresponding original node. Both the `next` and `random` pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list**.

For example, if there are two nodes `X` and `Y` in the original list, where `X.random --> Y`, then for the corresponding two nodes `x` and `y` in the copied list, `x.random --> y`.

Return _the head of the copied linked list_.

The linked list is represented in the input/output as a list of `n` nodes. Each node is represented as a pair of `[val, random_index]` where:

*   `val`: an integer representing `Node.val`
*   `random_index`: the index of the node (range from `0` to `n-1`) that the `random` pointer points to, or `null` if it does not point to any node.

Your code will **only** be given the `head` of the original linked list.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/12/18/e1.png)

**Input:** head = \[\[7,null],[13,0],[11,4],[10,2],[1,0]]

**Output:** [[7,null],[13,0],[11,4],[10,2],[1,0]] 

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/12/18/e2.png)

**Input:** head = \[\[1,1],[2,1]]

**Output:** [[1,1],[2,1]] 

**Example 3:**

**![](https://assets.leetcode.com/uploads/2019/12/18/e3.png)**

**Input:** head = \[\[3,null],[3,0],[3,null]]

**Output:** [[3,null],[3,0],[3,null]] 

**Example 4:**

**Input:** head = []

**Output:** []

**Explanation:** The given linked list is empty (null pointer), so return null. 

**Constraints:**

*   `0 <= n <= 1000`
*   `-10000 <= Node.val <= 10000`
*   `Node.random` is `null` or is pointing to some node in the linked list.

## Solution

```ruby
require_relative '../../com_github_leetcode/random/node'

# Definition for Node.
# class Node
#     attr_accessor :val, :next, :random
#     def initialize(val = 0)
#         @val = val
#		  @next = nil
#		  @random = nil
#     end
# end

# @param {Node} node
# @return {Node}
def copyRandomList(head)
  return nil if head.nil?

  # First pass to create cloned nodes and insert them after the original nodes
  curr = head
  while curr
    cloned_node = Node.new(curr.val)
    cloned_node.next = curr.next
    curr.next = cloned_node
    curr = cloned_node.next
  end

  # Second pass to set the random pointers of the cloned nodes
  curr = head
  while curr
    curr.next.random = curr.random.next if curr.random
    curr = curr.next.next
  end

  # Third pass to separate the original and cloned nodes
  curr = head
  new_head = nil
  while curr
    cloned_node = curr.next
    new_head ||= cloned_node
    curr.next = cloned_node.next
    cloned_node.next = curr.next.next if curr.next
    curr = curr.next
  end

  new_head
end
```