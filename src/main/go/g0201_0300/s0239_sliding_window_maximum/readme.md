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

```golang
func maxSlidingWindow(nums []int, k int) []int {
	if k == 1 {
		return nums
	}
	i := 1
	prev := nums
	var reuse []int
	for ; (1 << i) <= k; i++ {
		next := maxReduce(prev, 1<<(i-1), reuse)
		reuse = prev
		prev = next
	}
	if 1<<i == k {
		return prev
	}
	diff := k - (1 << (i - 1))
	return maxReduce(prev, diff, nil)[:len(nums)-k+1]
}

func maxReduce(nums []int, skip int, reuse []int) []int {
	// reuse allows to reuse prior allocations
	n := len(nums)
	var result []int
	if reuse != nil {
		result = reuse
	} else {
		result = make([]int, n-skip)
	}
	for i := 0; i < n-skip; i++ {
		result[i] = max(nums[i], nums[i+skip])
	}
	return result[:n-skip]
}
```