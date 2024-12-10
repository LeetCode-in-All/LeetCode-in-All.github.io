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

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
const mergeKLists = function(lists) {
    if (lists.length === 0) {
        return null
    }
    return mergeKListsHelper(lists, 0, lists.length)
};

const mergeKListsHelper = function(lists, leftIndex, rightIndex) {
    if (rightIndex > leftIndex + 1) {
        const mid = Math.floor((leftIndex + rightIndex) / 2)
        const left = mergeKListsHelper(lists, leftIndex, mid)
        const right = mergeKListsHelper(lists, mid, rightIndex)
        return mergeTwoLists(left, right)
    } else {
        return lists[leftIndex]
    }
};

const mergeTwoLists = function(left, right) {
    if (left === null) {
        return right
    }
    if (right === null) {
        return left
    }
    let res;
    if (left.val <= right.val) {
        res = left
        left = left.next
    } else {
        res = right
        right = right.next
    }
    let current = res;
    while (left !== null && right !== null) {
        if (left.val <= right.val) {
            current.next = left;
            left = left.next;
        } else {
            current.next = right;
            right = right.next;
        }
        current = current.next;
    }
    current.next = left !== null ? left : right;
    return res
};

export { mergeKLists }
```