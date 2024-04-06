[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 96\. Unique Binary Search Trees

Medium

Given an integer `n`, return _the number of structurally unique **BST'**s (binary search trees) which has exactly_ `n` _nodes of unique values from_ `1` _to_ `n`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

**Input:** n = 3

**Output:** 5 

**Example 2:**

**Input:** n = 1

**Output:** 1 

**Constraints:**

*   `1 <= n <= 19`

## Solution

```typescript
function numTrees(n: number): number {
    const uniqueCount = new Array(n + 1).fill(0)
    uniqueCount[0] = 1
    uniqueCount[1] = 1
    for (let i = 2; i <= n; ++i) {
        for (let j = 1; j <= i; ++j) {
            uniqueCount[i] += uniqueCount[j - 1] * uniqueCount[i - j]
        }
    }
    return uniqueCount[n]
}

export { numTrees }
```