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

```dart
class MedianFinder {
  PriorityQueue<int> small = PriorityQueue((a, b) =>b.compareTo(a));
  PriorityQueue<int> large = PriorityQueue();
  bool even = true;

  double findMedian() =>
  even ?(small.first +large.first)/2.0:small.first.toDouble();

  void addNum(int num) {
    if (even) {
      large.add(num);
      small.add(large.removeFirst());
    } else {
      small.add(num);
      large.add(small.removeFirst());
    }
    even = !even;
  }
}

// Priority Queue if not using package:collection/collection.dart
class PriorityQueue<E extends Comparable<dynamic>> {
  PriorityQueue([int Function(E, E)?comparison])
          :comparison =comparison ??Comparable.compare;

  final List<E> _queue = [];
  final Comparator<E> comparison;
  bool get
  isEmpty =>_queue.isEmpty;
  int get
  length =>_queue.length;
  E get
  first =>_queue.first;

  void add(E value) {
    _queue.add(value);
    var child = length - 1;
    var parent = _parentOf(child);
    while (child > 0 && child == _higherPriority(child, parent)) {
      _swapElements(child, parent);
      child = parent;
      parent = _parentOf(child);
    }
  }

  E removeFirst() {
    if (isEmpty) throw StateError('No element');
    _swapElements(0, length - 1);
    final firstElement =_queue.removeLast();
    var parentIndex = 0;
    while (true) {
      final leftIndex =_leftChildOf(parentIndex);
      final rightIndex =_rightChildOf(parentIndex);
      var chosen = _higherPriority(leftIndex, parentIndex);
      chosen = _higherPriority(rightIndex, chosen);
      if (chosen == parentIndex) break;
      _swapElements(parentIndex, chosen);
      parentIndex = chosen;
    }
    return firstElement;
  }

  int _leftChildOf(int parentIndex) =>2*parentIndex +1;

  int _rightChildOf(int parentIndex) =>2*parentIndex +2;

  int _parentOf(int childIndex) =>(childIndex -1)~/2;

  int _higherPriority(int index1, int index2) {
    if (index1 >= length) return index2;
    final value1 =_queue[index1];
    final value2 =_queue[index2];
    return comparison(value1, value2).isNegative ? index1 : index2;
  }

  void _swapElements(int index1, int index2) {
    final temp =_queue[index1];
    _queue[index1] = _queue[index2];
    _queue[index2] = temp;
  }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = MedianFinder();
 * obj.addNum(num);
 * double param2 = obj.findMedian();
 */
```