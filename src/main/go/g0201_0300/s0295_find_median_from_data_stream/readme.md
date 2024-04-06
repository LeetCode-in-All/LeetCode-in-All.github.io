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

```golang
func pushHeap(a *[]int, x int) {
	*a = append(*a, x)
	c := len(*a) - 1
	p := (c - 1) >> 1
	for 0 < c && (*a)[p] < (*a)[c] {
		(*a)[p], (*a)[c] = (*a)[c], (*a)[p]
		c = p
		p = (c - 1) >> 1
	}
}

func heapify(a []int, i int) {
	size := len(a)

	for i < size-1 {
		lc := min(size-1, (i<<1)+1)
		rc := min(size-1, (i<<1)+2)
		mc := lc
		if a[lc] < a[rc] {
			mc = rc
		}
		if a[mc] < a[i] {
			return
		}
		a[mc], a[i] = a[i], a[mc]
		i = mc
	}
}

func popHeap(a *[]int) int {
	size := len(*a)
	top := (*a)[0]
	(*a)[0], (*a)[size-1] = (*a)[size-1], (*a)[0]
	*a = (*a)[:size-1]
	heapify(*a, 0)
	return top
}

type MedianFinder struct {
	a []int
	b []int
}

func Constructor() MedianFinder {
	var obj MedianFinder
	return obj
}

func (this *MedianFinder) AddNum(num int) {
	if len(this.a) == 0 || num < this.a[0] {
		pushHeap(&this.a, num)
		if 1+len(this.b) < len(this.a) {
			pushHeap(&this.b, -popHeap(&this.a))
		}
	} else {
		pushHeap(&this.b, -num)
		if 1+len(this.a) < len(this.b) {
			pushHeap(&this.a, -popHeap(&this.b))
		}
	}
}

func (this *MedianFinder) FindMedian() float64 {
	if len(this.a) == len(this.b) {
		return (float64(this.a[0]) - float64(this.b[0])) * 0.5
	} else if len(this.a) < len(this.b) {
		return -float64(this.b[0])
	} else {
		return float64(this.a[0])
	}
}
```