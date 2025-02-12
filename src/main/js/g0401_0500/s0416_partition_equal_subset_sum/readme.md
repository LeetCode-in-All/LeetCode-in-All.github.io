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

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var canPartition = function(nums) {
    let sum = nums.reduce((acc, val) => acc + val, 0)
    if (sum % 2 !== 0) {
        return false
    }
    sum /= 2
    
    const set = new Array(sum + 1).fill(false)
    const arr = new Array(sum + 2).fill(0)
    let top = 0

    for (let val of nums) {
        for (let i = top; i >= 0; i--) {
            const tempSum = val + arr[i]
            if (tempSum <= sum && !set[tempSum]) {
                if (tempSum === sum) {
                    return true
                }
                set[tempSum] = true
                arr[++top] = tempSum
            }
        }
    }

    return false
};

export { canPartition }
```