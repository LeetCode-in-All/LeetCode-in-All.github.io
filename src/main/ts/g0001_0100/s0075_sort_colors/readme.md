[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 75\. Sort Colors

Medium

Given an array `nums` with `n` objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

**Example 1:**

**Input:** nums = [2,0,2,1,1,0]

**Output:** [0,0,1,1,2,2] 

**Example 2:**

**Input:** nums = [2,0,1]

**Output:** [0,1,2] 

**Example 3:**

**Input:** nums = [0]

**Output:** [0] 

**Example 4:**

**Input:** nums = [1]

**Output:** [1] 

**Constraints:**

*   `n == nums.length`
*   `1 <= n <= 300`
*   `nums[i]` is `0`, `1`, or `2`.

**Follow up:** Could you come up with a one-pass algorithm using only constant extra space?

## Solution

```typescript
const sortColors = (nums: number[]) => {
    let i = 0
    let num2s = 0
    while (i < nums.length) {
        const num = nums.shift()
        if (num === 0) nums.splice(nums.length - i, 0, 0)
        else if (num === 1) nums.splice(nums.length - num2s, 0, 1)
        else {
            num2s++
            nums.push(2)
        }
        i++
    }
}

export { sortColors }
```