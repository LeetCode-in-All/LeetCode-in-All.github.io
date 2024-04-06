[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 19\. Remove Nth Node From End of List

Medium

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

**Input:** head = [1,2,3,4,5], n = 2

**Output:** [1,2,3,5] 

**Example 2:**

**Input:** head = [1], n = 1

**Output:** [] 

**Example 3:**

**Input:** head = [1,2], n = 1

**Output:** [1] 

**Constraints:**

*   The number of nodes in the list is `sz`.
*   `1 <= sz <= 30`
*   `0 <= Node.val <= 100`
*   `1 <= n <= sz`

**Follow up:** Could you do this in one pass?

## Solution

```php
use leetcode\com_github_leetcode\ListNode;

/*
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
    private $n;

    /**
     * @param ListNode $head
     * @param Integer $n
     * @return ListNode
     */
    public function removeNthFromEnd($head, $n) {
        $this->n = $n;
        $node = new ListNode(0, $head);
        $this->removeNth($node);
        return $node->next;
    }

    private function removeNth($node) {
        if ($node->next === null) {
            return;
        }
        $this->removeNth($node->next);
        $this->n--;
        if ($this->n == 0) {
            $node->next = $node->next->next;
        }
    }
}
```