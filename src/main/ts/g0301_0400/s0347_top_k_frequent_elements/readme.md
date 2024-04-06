[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 347\. Top K Frequent Elements

Medium

Given an integer array `nums` and an integer `k`, return _the_ `k` _most frequent elements_. You may return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,1,1,2,2,3], k = 2

**Output:** [1,2]

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1]

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   `k` is in the range `[1, the number of unique elements in the array]`.
*   It is **guaranteed** that the answer is **unique**.

**Follow up:** Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.

## Solution

```typescript
function topKFrequent(nums: number[], k: number): number[] {
    let elementCount = new Array<number[]>(nums.length)
    let hashMap = new Map<number, number>()
    let res: number[] = new Array()
    nums.forEach((num) => {
        if (!hashMap.has(num)) hashMap.set(num, 1)
        else hashMap.set(num, hashMap.get(num)! + 1)
    })
    hashMap.forEach((value, key) => {
        if (elementCount[value] === undefined) elementCount[value] = [key]
        else elementCount[value].push(key)
    })
    for (let i = elementCount.length - 1; i >= 0; i--) {
        if (elementCount[i] !== undefined) res.push(...elementCount[i].values())
        if (res.length === k) {
            return res
        }
    }
    return res
}

export { topKFrequent }
```