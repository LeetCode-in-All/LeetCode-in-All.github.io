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

```golang
import "container/heap"


type ListNode struct {
	Val  int
	Next *ListNode
}

/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func mergeKLists(lists []*ListNode) *ListNode {
	var h minHeap
	for _, node := range lists {
		for node != nil {
			h = append(h, node)
			node = node.Next
		}
	}
	heap.Init(&h)

	if len(h) == 0 {
		return nil
	}

	res := heap.Pop(&h).(*ListNode)
	cur := res
	for h.Len() > 0 {
		cur.Next = heap.Pop(&h).(*ListNode)
		cur.Next.Next = nil
		cur = cur.Next
	}

	return res
}

type minHeap []*ListNode

func (h minHeap) Len() int           { return len(h) }
func (h minHeap) Less(i, j int) bool { return h[i].Val <= h[j].Val }
func (h minHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *minHeap) Push(val any) {
	*h = append(*h, val.(*ListNode))
}

func (h *minHeap) Pop() any {
	res := (*h)[len(*h)-1]
	*h = (*h)[:len(*h)-1]
	return res
}
```