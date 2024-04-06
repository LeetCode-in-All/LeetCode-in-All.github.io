[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 31\. Next Permutation

Medium

A **permutation** of an array of integers is an arrangement of its members into a sequence or linear order.

-   For example, for `arr = [1,2,3]`, the following are all the permutations of `arr`: `[1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1]`.

The **next permutation** of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the **next permutation** of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

-   For example, the next permutation of `arr = [1,2,3]` is `[1,3,2]`.
-   Similarly, the next permutation of `arr = [2,3,1]` is `[3,1,2]`.
-   While the next permutation of `arr = [3,2,1]` is `[1,2,3]` because `[3,2,1]` does not have a lexicographical larger rearrangement.

Given an array of integers `nums`, _find the next permutation of_ `nums`.

The replacement must be **[in place](http://en.wikipedia.org/wiki/In-place_algorithm)** and use only constant extra memory.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [1,3,2]

**Example 2:**

**Input:** nums = [3,2,1]

**Output:** [1,2,3]

**Example 3:**

**Input:** nums = [1,1,5]

**Output:** [1,5,1]

**Constraints:**

-   `1 <= nums.length <= 100`
-   `0 <= nums[i] <= 100`

## Solution

```typescript
/*
 Do not return anything, modify nums in-place instead.
 */
function nextPermutation(nums: number[]): void {
    let swapperIndex: number | null = null

    for (let ind = nums.length - 1; ind >= 0 && swapperIndex == null; ind--) {
        if (nums[ind] > nums[ind - 1]) {
            swapperIndex = ind - 1
        }
    }

    if (swapperIndex == null) nums.sort((a, b) => a - b)
    else {
        nums.splice(swapperIndex + 1, nums.length, ...nums.slice(swapperIndex + 1, nums.length).sort((a, b) => a - b))
        let indToBringForward = swapperIndex + 1
        while (nums[indToBringForward] <= nums[swapperIndex]) ++indToBringForward
        let swappedNumber = nums[swapperIndex]
        nums[swapperIndex] = nums[indToBringForward]
        nums[indToBringForward] = swappedNumber
    }
}

export { nextPermutation }
```