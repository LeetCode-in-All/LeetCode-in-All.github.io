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
     * @param ListNode $list1
     * @param ListNode $list2
     * @return ListNode
     */
    public function mergeTwoLists($l1, $l2) {
        $list = new ListNode(-1);
        $head = $list;
        while ($l1 !== null || $l2 !== null) {
            if ($l1 !== null && $l2 !== null) {
                if ($l1->val <= $l2->val) {
                    $list->next = new ListNode($l1->val);
                    $l1 = $l1->next;
                } else {
                    $list->next = new ListNode($l2->val);
                    $l2 = $l2->next;
                }
            } elseif ($l1 !== null) {
                $list->next = new ListNode($l1->val);
                $l1 = $l1->next;
            } else {
                $list->next = new ListNode($l2->val);
                $l2 = $l2->next;
            }

            $list = $list->next;
        }
        return $head->next;
    }
}
```