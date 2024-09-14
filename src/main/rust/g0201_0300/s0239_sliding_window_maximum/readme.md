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

```rust
use std::collections::VecDeque;

struct MaxQueue {
    queue: VecDeque<i32>,
}

impl MaxQueue {
    fn new() -> Self {
        Self {
            queue: VecDeque::new(),
        }
    }

    fn enqueue(&mut self, element: i32) {
        while !self.queue.is_empty() && *self.queue.back().unwrap() < element {
            self.queue.pop_back();
        }
        self.queue.push_back(element);
    }

    fn dequeue(&mut self, removed_element: i32) -> i32 {
        if !self.queue.is_empty() && *self.queue.front().unwrap() == removed_element {
            self.queue.pop_front().unwrap()
        } else {
            removed_element
        }
    }

    // Get the maximum element in the queue
    fn get_max(&self) -> Option<i32> {
        self.queue.front().copied()
    }
}

impl Solution {
    pub fn max_sliding_window(nums: Vec<i32>, k: i32) -> Vec<i32> {
        let k = k as usize;
        let n = nums.len();
        let mut max_queue = MaxQueue::new();
        let mut result: Vec<i32> = vec![0; n - k + 1];

        // Fill initial window in the MaxQueue
        for i in 0..k {
            max_queue.enqueue(nums[i]);
        }

        // Calculate maximum for each window
        for i in k..n {
            // Get maximum from MaxQueue
            result[i - k] = max_queue.get_max().unwrap();

            // Move window by dequeuing the element leaving the window
            max_queue.dequeue(nums[i - k]);

            // Add the current element to the MaxQueue
            max_queue.enqueue(nums[i]);
        }

        // Get the maximum for the last window
        result[n - k] = max_queue.get_max().unwrap();

        result
    }
}
```