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

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int* maxHeap;
    int maxHeapSize;
    int maxHeapCapacity;

    int* minHeap;
    int minHeapSize;
    int minHeapCapacity;
} MedianFinder;

MedianFinder* medianFinderCreate() {
    MedianFinder* obj = (MedianFinder*)malloc(sizeof(MedianFinder));

    obj->maxHeapCapacity = 10;  // Initial capacity for maxHeap
    obj->maxHeapSize = 0;
    obj->maxHeap = (int*)malloc(obj->maxHeapCapacity * sizeof(int));

    obj->minHeapCapacity = 10;  // Initial capacity for minHeap
    obj->minHeapSize = 0;
    obj->minHeap = (int*)malloc(obj->minHeapCapacity * sizeof(int));

    return obj;
}

// Helper functions for max-heap and min-heap
void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Max-Heap functions
void maxHeapPush(MedianFinder* obj, int value) {
    if (obj->maxHeapSize == obj->maxHeapCapacity) {
        obj->maxHeapCapacity *= 2;
        obj->maxHeap = (int*)realloc(obj->maxHeap, obj->maxHeapCapacity * sizeof(int));
    }
    obj->maxHeap[obj->maxHeapSize++] = value;

    // Sift-up
    int i = obj->maxHeapSize - 1;
    while (i > 0 && obj->maxHeap[(i - 1) / 2] < obj->maxHeap[i]) {
        swap(&obj->maxHeap[(i - 1) / 2], &obj->maxHeap[i]);
        i = (i - 1) / 2;
    }
}

int maxHeapPop(MedianFinder* obj) {
    int result = obj->maxHeap[0];
    obj->maxHeap[0] = obj->maxHeap[--obj->maxHeapSize];

    // Sift-down
    int i = 0;
    while (2 * i + 1 < obj->maxHeapSize) {
        int j = 2 * i + 1;
        if (j + 1 < obj->maxHeapSize && obj->maxHeap[j + 1] > obj->maxHeap[j]) {
            j++;
        }
        if (obj->maxHeap[i] >= obj->maxHeap[j]) break;
        swap(&obj->maxHeap[i], &obj->maxHeap[j]);
        i = j;
    }
    return result;
}

int maxHeapTop(MedianFinder* obj) {
    return obj->maxHeap[0];
}

// Min-Heap functions
void minHeapPush(MedianFinder* obj, int value) {
    if (obj->minHeapSize == obj->minHeapCapacity) {
        obj->minHeapCapacity *= 2;
        obj->minHeap = (int*)realloc(obj->minHeap, obj->minHeapCapacity * sizeof(int));
    }
    obj->minHeap[obj->minHeapSize++] = value;

    // Sift-up
    int i = obj->minHeapSize - 1;
    while (i > 0 && obj->minHeap[(i - 1) / 2] > obj->minHeap[i]) {
        swap(&obj->minHeap[(i - 1) / 2], &obj->minHeap[i]);
        i = (i - 1) / 2;
    }
}

int minHeapPop(MedianFinder* obj) {
    int result = obj->minHeap[0];
    obj->minHeap[0] = obj->minHeap[--obj->minHeapSize];

    // Sift-down
    int i = 0;
    while (2 * i + 1 < obj->minHeapSize) {
        int j = 2 * i + 1;
        if (j + 1 < obj->minHeapSize && obj->minHeap[j + 1] < obj->minHeap[j]) {
            j++;
        }
        if (obj->minHeap[i] <= obj->minHeap[j]) break;
        swap(&obj->minHeap[i], &obj->minHeap[j]);
        i = j;
    }
    return result;
}

int minHeapTop(MedianFinder* obj) {
    return obj->minHeap[0];
}

// Balancing the heaps
void balanceHeaps(MedianFinder* obj) {
    if (obj->maxHeapSize > obj->minHeapSize + 1) {
        minHeapPush(obj, maxHeapPop(obj));
    } else if (obj->minHeapSize > obj->maxHeapSize) {
        maxHeapPush(obj, minHeapPop(obj));
    }
}

void medianFinderAddNum(MedianFinder* obj, int num) {
    if (obj->maxHeapSize == 0 || num <= maxHeapTop(obj)) {
        maxHeapPush(obj, num);
    } else {
        minHeapPush(obj, num);
    }
    balanceHeaps(obj);
}

double medianFinderFindMedian(MedianFinder* obj) {
    if (obj->maxHeapSize > obj->minHeapSize) {
        return maxHeapTop(obj);
    } else {
        return (maxHeapTop(obj) + minHeapTop(obj)) / 2.0;
    }
}

void medianFinderFree(MedianFinder* obj) {
    free(obj->maxHeap);
    free(obj->minHeap);
    free(obj);
}

/**
 * Your MedianFinder struct will be instantiated and called as such:
 * MedianFinder* obj = medianFinderCreate();
 * medianFinderAddNum(obj, num);
 
 * double param_2 = medianFinderFindMedian(obj);
 
 * medianFinderFree(obj);
*/
```