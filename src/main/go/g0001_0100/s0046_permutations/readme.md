[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 46\. Permutations

Medium

Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

**Example 2:**

**Input:** nums = [0,1]

**Output:** [[0,1],[1,0]]

**Example 3:**

**Input:** nums = [1]

**Output:** [[1]]

**Constraints:**

*   `1 <= nums.length <= 6`
*   `-10 <= nums[i] <= 10`
*   All the integers of `nums` are **unique**.

## Solution

```golang
func permute(nums []int) [][]int {
	if len(nums) == 0 {
		return [][]int{}
	}
	finalResult := [][]int{}
	permuteRecur(nums, &finalResult, []int{}, make([]bool, len(nums)))
	return finalResult
}

func permuteRecur(nums []int, finalResult *[][]int, currResult []int, used []bool) {
	if len(currResult) == len(nums) {
		temp := make([]int, len(currResult))
		copy(temp, currResult)
		*finalResult = append(*finalResult, temp)
		return
	}
	for i := 0; i < len(nums); i++ {
		if used[i] {
			continue
		}
		currResult = append(currResult, nums[i])
		used[i] = true
		permuteRecur(nums, finalResult, currResult, used)
		used[i] = false
		currResult = currResult[:len(currResult)-1]
	}
}
```