[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 45\. Jump Game II

Medium

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

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

## Solution

```typescript
function jump(nums: number[]): number { //NOSONAR
    let minJmp = new Array(nums.length)
    if (nums.length === 1) return 0
    let prevIndex = 0
    minJmp[prevIndex] = 0
    while (prevIndex < nums.length - 1) {
        let nextMaxJmpTo = nums[prevIndex] + prevIndex
        let prevIndexJmp = minJmp[prevIndex]

        let farthestJumpVal = -1
        let farthestJumpIndex = -1
        for (let i = nextMaxJmpTo; ; i--) {
            if (i >= nums.length) {
                continue
            }
            if (i === nums.length - 1) {
                return prevIndexJmp + 1
            }
            if (minJmp[i] != undefined) {
                break
            }
            minJmp[i] = prevIndexJmp + 1
            let curmaxTo = nums[i] + i
            if (farthestJumpVal < curmaxTo) {
                farthestJumpVal = curmaxTo
                farthestJumpIndex = i
            }
        }
        if (farthestJumpIndex === -1) {
            return -1
        }
        prevIndex = farthestJumpIndex
    }
    return minJmp[nums.length - 1]
}

export { jump }
```