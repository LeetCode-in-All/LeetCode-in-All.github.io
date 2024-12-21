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

```javascript
var MedianFinder = function () {
    this.large = new Heap();
    this.small = new Heap();
};

/** 
 * @param {number} num
 * @return {void}
 */
MedianFinder.prototype.addNum = function (num) {
    if (this.small.length() === this.large.length()) {
        this.small.push(-num);
        this.large.push(-this.small.pop());
    } else {
        this.large.push(num);
        this.small.push(-this.large.pop());
    }
};

/**
 * @return {number}
 */
MedianFinder.prototype.findMedian = function () {
    if (this.small.length() === this.large.length()) {
        return (this.large.peek() - this.small.peek()) / 2;
    }
    return this.large.peek();
};

/**
 * Heap implementation
 */
var Heap = function () {
    this.heap = [0];
};

Heap.prototype.peek = function () {
    return this.heap[1] ?? null;
};

Heap.prototype.push = function (val) {
    this.heap.push(val);
    let i = this.heap.length - 1;
    let parI = Math.floor(i / 2);
    while (i > 1 && this.heap[i] < this.heap[parI]) {
        const tmp = this.heap[i];
        this.heap[i] = this.heap[parI];
        this.heap[parI] = tmp;
        i = parI;
        parI = Math.floor(i / 2);
    }
};

Heap.prototype.pop = function () {
    if (this.heap.length === 1) {
        return null;
    }
    if (this.heap.length === 2) {
        return this.heap.pop();
    }
    const res = this.heap[1];
    this.heap[1] = this.heap.pop();
    let i = 1;
    while (2 * i < this.heap.length) {
        const leftChildIdx = 2 * i;
        const rightChildIdx = 2 * i + 1;
        if (
            rightChildIdx < this.heap.length &&
            this.heap[rightChildIdx] < this.heap[leftChildIdx] &&
            this.heap[i] > this.heap[rightChildIdx]
        ) {
            const tmp = this.heap[i];
            this.heap[i] = this.heap[rightChildIdx];
            this.heap[rightChildIdx] = tmp;
            i = rightChildIdx;
        } else if (this.heap[i] > this.heap[leftChildIdx]) {
            const tmp = this.heap[i];
            this.heap[i] = this.heap[leftChildIdx];
            this.heap[leftChildIdx] = tmp;
            i = leftChildIdx;
        } else {
            break;
        }
    }
    return res;
};

Heap.prototype.length = function () {
    return this.heap.length - 1;
};

export { MedianFinder }
```