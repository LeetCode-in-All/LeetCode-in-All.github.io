[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 295\. Find Median from Data Stream

Hard

The **median** is the middle value in an ordered integer list. If the size of the list is even, there is no middle value and the median is the mean of the two middle values.

*   For example, for `arr = [2,3,4]`, the median is `3`.
*   For example, for `arr = [2,3]`, the median is `(2 + 3) / 2 = 2.5`.

Implement the MedianFinder class:

*   `MedianFinder()` initializes the `MedianFinder` object.
*   `void addNum(int num)` adds the integer `num` from the data stream to the data structure.
*   `double findMedian()` returns the median of all elements so far. Answers within <code>10<sup>-5</sup></code> of the actual answer will be accepted.

**Example 1:**

**Input**

    ["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
    [[], [1], [2], [], [3], []]

**Output:** [null, null, null, 1.5, null, 2.0]

**Explanation:**

    MedianFinder medianFinder = new MedianFinder();
    medianFinder.addNum(1); // arr = [1]
    medianFinder.addNum(2); // arr = [1, 2]
    medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
    medianFinder.addNum(3); // arr[1, 2, 3]
    medianFinder.findMedian(); // return 2.0 

**Constraints:**

*   <code>-10<sup>5</sup> <= num <= 10<sup>5</sup></code>
*   There will be at least one element in the data structure before calling `findMedian`.
*   At most <code>5 * 10<sup>4</sup></code> calls will be made to `addNum` and `findMedian`.

**Follow up:**

*   If all integer numbers from the stream are in the range `[0, 100]`, how would you optimize your solution?
*   If `99%` of all integer numbers from the stream are in the range `[0, 100]`, how would you optimize your solution?

## Solution

```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

struct MedianFinder {
    max_heap: BinaryHeap<i32>,                // Max heap for lower half
    min_heap: BinaryHeap<Reverse<i32>>,       // Min heap for upper half
}

/**
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */

impl MedianFinder {
    /** Initialize your data structure here. */
    pub fn new() -> Self {
        MedianFinder {
            max_heap: BinaryHeap::new(),                // Max heap (lower half)
            min_heap: BinaryHeap::new(),                // Min heap (upper half), with Reverse for min behavior
        }
    }

    /** Add a number to the data structure */
    pub fn add_num(&mut self, num: i32) {
        if self.max_heap.is_empty() || *self.max_heap.peek().unwrap() > num {
            self.max_heap.push(num);  // Add to the max heap (lower half)
        } else {
            self.min_heap.push(Reverse(num));  // Add to the min heap (upper half)
        }

        // Balance the two heaps
        if (self.max_heap.len() as i32 - self.min_heap.len() as i32).abs() > 1 {
            self.balance();
        }
    }

    /** Balance the heaps */
    fn balance(&mut self) {
        if self.max_heap.len() > self.min_heap.len() {
            self.min_heap.push(Reverse(self.max_heap.pop().unwrap()));
        } else {
            self.max_heap.push(self.min_heap.pop().unwrap().0);
        }
    }

    /** Find the median of the numbers added so far */
    pub fn find_median(&self) -> f64 {
        if self.max_heap.len() == self.min_heap.len() {
            (*self.max_heap.peek().unwrap() as f64 + self.min_heap.peek().unwrap().0 as f64) / 2.0
        } else if self.max_heap.len() > self.min_heap.len() {
            *self.max_heap.peek().unwrap() as f64
        } else {
            self.min_heap.peek().unwrap().0 as f64
        }
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * let obj = MedianFinder::new();
 * obj.add_num(num);
 * let ret_2: f64 = obj.find_median();
 */
```