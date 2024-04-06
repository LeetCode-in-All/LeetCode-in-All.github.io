[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 416\. Partition Equal Subset Sum

Medium

Given a **non-empty** array `nums` containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Example 1:**

**Input:** nums = [1,5,11,5]

**Output:** true

**Explanation:** The array can be partitioned as [1, 5, 5] and [11]. 

**Example 2:**

**Input:** nums = [1,2,3,5]

**Output:** false

**Explanation:** The array cannot be partitioned into equal sum subsets. 

**Constraints:**

*   `1 <= nums.length <= 200`
*   `1 <= nums[i] <= 100`

## Solution

```typescript
function canPartition(nums: number[]): boolean {
    let sums: number = 0
    for (const num of nums) {
        sums += num
    }
    if (sums % 2 === 1) {
        return false
    }
    sums /= 2
    const dp: boolean[] = new Array(sums + 1).fill(false)
    dp[0] = true
    for (const num of nums) {
        for (let sum = sums; sum >= num; sum--) {
            dp[sum] = dp[sum] || dp[sum - num]
        }
    }
    return dp[sums]
}

export { canPartition }
```