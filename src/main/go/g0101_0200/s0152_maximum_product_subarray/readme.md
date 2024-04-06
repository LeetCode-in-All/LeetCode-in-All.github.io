[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 152\. Maximum Product Subarray

Medium

Given an integer array `nums`, find a contiguous non-empty subarray within the array that has the largest product, and return _the product_.

The test cases are generated so that the answer will fit in a **32-bit** integer.

A **subarray** is a contiguous subsequence of the array.

**Example 1:**

**Input:** nums = [2,3,-2,4]

**Output:** 6

**Explanation:** [2,3] has the largest product 6.

**Example 2:**

**Input:** nums = [-2,0,-1]

**Output:** 0

**Explanation:** The result cannot be 2, because [-2,-1] is not a subarray.

**Constraints:**

*   <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
*   `-10 <= nums[i] <= 10`
*   The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

## Solution

```golang
func maxProduct(nums []int) int {
	res := findMax(nums...)
	min, max := 1, 1

	for _, n := range nums {
		if n == 0 {
			min, max = 1, 1
			continue
		}
		buffer := max * n
		max = findMax(n*max, n*min, n)
		min = findMin(buffer, n*min, n)

		res = findMax(res, max)
	}
	return res
}

func findMax(nums ...int) int {
	highest := nums[0]
	for _, n := range nums {
		if n > highest {
			highest = n
		}
	}
	return highest
}

func findMin(nums ...int) int {
	lowest := nums[0]
	for _, n := range nums {
		if n < lowest {
			lowest = n
		}
	}
	return lowest
}
```