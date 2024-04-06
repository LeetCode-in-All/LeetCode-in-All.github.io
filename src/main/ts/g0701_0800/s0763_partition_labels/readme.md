[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 763\. Partition Labels

Medium

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Return _a list of integers representing the size of these parts_.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"

**Output:** [9,7,8]

**Explanation:**

    The partition is "ababcbaca", "defegde", "hijhklij".
    This is a partition so that each letter appears in at most one part.
    A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts. 

**Example 2:**

**Input:** s = "eccbbbbdec"

**Output:** [10] 

**Constraints:**

*   `1 <= s.length <= 500`
*   `s` consists of lowercase English letters.

## Solution

```typescript
function partitionLabels(s: string): number[] {
    const map = new Map<string, [number, number]>()
    for (let i = 0; i < s.length; i++) {
        const c = s[i]
        if (!map.has(c)) map.set(c, [i, i])
        else map.get(c)[1] = i
    }
    const arr = Array.from(map.values())
    arr.sort((v1, v2) => v1[0] - v2[0])
    let start = 0,
        end = arr[0][1],
        result: number[] = []
    for (let i = 1; i < arr.length; i++) {
        if (arr[i][0] < end) end = Math.max(end, arr[i][1])
        else {
            result.push(end - start + 1)
            start = arr[i][0]
            end = arr[i][1]
        }
    }
    result.push(end - start + 1)
    return result
}

export { partitionLabels }
```