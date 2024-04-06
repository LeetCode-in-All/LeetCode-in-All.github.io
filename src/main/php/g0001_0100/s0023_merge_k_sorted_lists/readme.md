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

```php
use leetcode\com_github_leetcode\ListNode;

/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val = 0, $next = null) {
 *         $this->val = $val;
 *         $this->next = $next;
 *     }
 * }
 */
class Solution {
    /**
     * @param ListNode[] $lists
     * @return ListNode
     */
    public function mergeKLists($lists) {
        $heap = new \SplMinHeap();
        $head = [];
        foreach ($lists as $list) {
            $head = $list;
            while ($head) {
                $heap->insert($head->val);
                $head = $head->next;
            }
        }
        if (!$heap->isEmpty()) {
            $head = new ListNode($heap->extract());
            $curr = $head;
            while ($heap->valid()) {
                $node = new ListNode($heap->extract());
                $curr->next = $node;
                $curr = $node;
            }
        }
        return $head;
    }
}
```