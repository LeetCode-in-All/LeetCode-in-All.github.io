[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 239\. Sliding Window Maximum

Hard

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

**Example 1:**

**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3

**Output:** [3,3,5,5,6,7]

**Explanation:** 

Window position Max 

--------------- ----- 

[1 3 -1] -3 5 3 6 7 **3** 

1 [3 -1 -3] 5 3 6 7 **3** 

1 3 [-1 -3 5] 3 6 7 **5** 

1 3 -1 [-3 5 3] 6 7 **5** 

1 3 -1 -3 [5 3 6] 7 **6** 

1 3 -1 -3 5 [3 6 7] **7**

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1]

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `1 <= k <= nums.length`

## Solution

```dart
import 'dart:collection';

class Solution {
  List<int> maxSlidingWindow(List<int> nums, int k) {
    int n = nums.length;
    List<int> res = List.filled(n - k + 1, 0);
    int x = 0;
    Queue<int> dq = Queue();
    int i = 0;
    int j = 0;

    while (j < nums.length) {
      // Remove elements from the deque that are smaller than the current element
      while (dq.isNotEmpty && dq.last < nums[j]) {
        dq.removeLast();
      }

      // Add the current element to the deque
      dq.addLast(nums[j]);

      // When the window size reaches k
      if (j - i + 1 == k) {
        // The element at the front of the deque is the largest in the current window
        res[x] = dq.first;
        x++;

        // If the element at the front of the deque is going out of the window, remove it
        if (dq.first == nums[i]) {
          dq.removeFirst();
        }

        // Slide the window to the right
        i++;
      }

      j++;
    }

    return res;
  }
}
```