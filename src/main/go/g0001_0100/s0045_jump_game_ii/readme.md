[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 45\. Jump Game II

Medium

You are given a **0-indexed** array of integers `nums` of length `n`. You are initially positioned at `nums[0]`.

Each element `nums[i]` represents the maximum length of a forward jump from index `i`. In other words, if you are at `nums[i]`, you can jump to any `nums[i + j]` where:

*   `0 <= j <= nums[i]` and
*   `i + j < n`

Return _the minimum number of jumps to reach_ `nums[n - 1]`. The test cases are generated such that you can reach `nums[n - 1]`.

**Example 1:**

**Input:** nums = [2,3,1,1,4]

**Output:** 2

**Explanation:** The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index. 

**Example 2:**

**Input:** nums = [2,3,0,1,4]

**Output:** 2 

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   `0 <= nums[i] <= 1000`
*   It's guaranteed that you can reach `nums[n - 1]`.

## Solution

```golang
func jump(nums []int) int {
	length := 0
	maxLength := 0
	minJump := 0
	for i := 0; i < len(nums)-1; i++ {
		length--
		maxLength--
		maxLength = max(maxLength, nums[i])
		if length <= 0 {
			length = maxLength
			minJump++
		}
		if length >= len(nums)-i-1 {
			return minJump
		}
	}
	return minJump
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```