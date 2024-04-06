[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 41\. First Missing Positive

Hard

Given an unsorted integer array `nums`, return the smallest missing positive integer.

You must implement an algorithm that runs in `O(n)` time and uses constant extra space.

**Example 1:**

**Input:** nums = [1,2,0]

**Output:** 3

**Explanation:** The numbers in the range [1,2] are all in the array.

**Example 2:**

**Input:** nums = [3,4,-1,1]

**Output:** 2

**Explanation:** 1 is in the array but 2 is missing.

**Example 3:**

**Input:** nums = [7,8,9,11,12]

**Output:** 1

**Explanation:** The smallest positive integer 1 is missing.

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>

## Solution

```golang
func firstMissingPositive(nums []int) int {
	for i := 0; i < len(nums); i++ {
		if nums[i] < 0 {
			nums[i] = 0
		}
	}

	for i := 0; i < len(nums); i++ {
		val := abs(nums[i])
		if val > 0 && val <= len(nums) {
			if nums[val-1] > 0 {
				nums[val-1] = nums[val-1] * -1
				continue
			}

			if nums[val-1] == 0 {
				nums[val-1] = -1 * (len(nums) + 1)
			}
		}
	}

	for i := 1; i <= len(nums); i++ {
		if nums[i-1] >= 0 {
			return i
		}
	}

	return len(nums) + 1
}

func abs(n int) int {
	if n >= 0 {
		return n
	}

	return n * -1
}
```