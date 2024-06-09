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

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        if len(lists) == 0:
            return ListNode().next
        else:
            cnt = 0
            n = len(lists)

            first = ListNode()
            temp = first
            while cnt < n:
                temp.next = lists[cnt]
                while temp.next is not None:
                    temp = temp.next
                cnt +=1
            return self.list_to_linked_list(self.linked_list_to_list(first.next))

    def linked_list_to_list(self,head):
        if head == None:
            return 
        else:
            l = []
            temp = head
            while temp is not None:
                l.append(temp.val)
                temp = temp.next
            return sorted(l)

    def list_to_linked_list(self,l):
        if l == None:
            return
        first = ListNode()
        temp = first
        for i in l:
            node = ListNode(i)
            temp.next = node
            temp = temp.next
        return first.next
```