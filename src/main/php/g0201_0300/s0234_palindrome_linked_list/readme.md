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

```php
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
     * @return Boolean
     */
    public function isPalindrome($head) {
        $array = [];
        while ($head) {
            $array[] = $head->val;
            $head = $head->next;
        }
        $cnt = count($array);
        for ($x = 0; $x < $cnt / 2; $x++) {
            $yKey = $cnt - 1 - $x;

            if ($array[$x] !== $array[$yKey]) {
                return false;
            }
        }
        return true;
    }
}
```