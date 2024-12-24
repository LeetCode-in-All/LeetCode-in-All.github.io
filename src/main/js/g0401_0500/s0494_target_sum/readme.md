[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 494\. Target Sum

Medium

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

*   For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

**Example 1:**

**Input:** nums = [1,1,1,1,1], target = 3

**Output:** 5

**Explanation:** There are 5 ways to assign symbols to make the sum of nums be target 3. 

-1 + 1 + 1 + 1 + 1 = 3 

+1 - 1 + 1 + 1 + 1 = 3 

+1 + 1 - 1 + 1 + 1 = 3 

+1 + 1 + 1 - 1 + 1 = 3 

    +1 + 1 + 1 + 1 - 1 = 3

**Example 2:**

**Input:** nums = [1], target = 1

**Output:** 1

**Constraints:**

*   `1 <= nums.length <= 20`
*   `0 <= nums[i] <= 1000`
*   `0 <= sum(nums[i]) <= 1000`
*   `-1000 <= target <= 1000`

## Solution

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var findTargetSumWays = function(nums, target) {
    const n = nums.length
    let totalSum = 0
    for (let i = 0; i < n; i++) {
        totalSum += nums[i]
    }

    const sum = totalSum - target
    if (sum < 0 || sum % 2 === 1) {
        return 0
    }

    const targetSum = Math.floor(sum / 2)

    // Helper function to solve the problem
    const solve = (nums, target) => {
        let prev = new Array(target + 1).fill(0)

        if (nums[0] === 0) {
            prev[0] = 2 // Two ways to form sum 0: +0 and -0
        } else {
            prev[0] = 1
        }

        if (nums[0] !== 0 && nums[0] <= target) {
            prev[nums[0]] = 1
        }

        for (let i = 1; i < nums.length; i++) {
            const curr = new Array(target + 1).fill(0)
            for (let j = 0; j <= target; j++) {
                const taken = j >= nums[i] ? prev[j - nums[i]] : 0
                const nonTaken = prev[j]
                curr[j] = taken + nonTaken
            }
            prev = curr
        }

        return prev[target]
    }

    return solve(nums, targetSum)
};

export { findTargetSumWays }
```