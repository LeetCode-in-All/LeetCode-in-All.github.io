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
     * @param ListNode $head
     * @return ListNode
     */
    public function swapPairs($head) {
        $output = new ListNode(0);
        $output->next = $head;
        $point = $output;
        while ($point->next != null && $point->next->next != null) {
            $point1 = $point->next;
            $point2 = $point->next->next;
            $point->next = $point2;
            $point1->next = $point2->next;
            $point2->next = $point1;
            $point = $point1;
        }
        return $output->next;
    }
}
```