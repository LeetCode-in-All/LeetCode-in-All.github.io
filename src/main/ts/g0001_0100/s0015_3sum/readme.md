[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 15\. 3Sum

Medium

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

**Input:** nums = [-1,0,1,2,-1,-4]

**Output:** [[-1,-1,2],[-1,0,1]] 

**Example 2:**

**Input:** nums = []

**Output:** [] 

**Example 3:**

**Input:** nums = [0]

**Output:** [] 

**Constraints:**

*   `0 <= nums.length <= 3000`
*   <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>

## Solution

```typescript
function threeSum(nums: number[]): number[][] { //NOSONAR
    nums.sort((a, b) => a - b)
    const len = nums.length
    const result: number[][] = []
    let l: number
    let r: number
    for (let i = 0; i < len - 2; i++) {
        l = i + 1
        r = len - 1
        while (r > l) {
            const sum = nums[i] + nums[l] + nums[r]
            if (sum < 0) {
                l++
            } else if (sum > 0) {
                r--
            } else {
                const list: number[] = [nums[i], nums[l], nums[r]]
                result.push(list)
                while (l < r && nums[l + 1] === nums[l]) {
                    l++
                }
                while (r > l && nums[r - 1] === nums[r]) {
                    r--
                }
                l++
                r--
            }
        }
        while (i < len - 1 && nums[i + 1] === nums[i]) {
            i++ //NOSONAR
        }
    }
    return result
}

export { threeSum }
```