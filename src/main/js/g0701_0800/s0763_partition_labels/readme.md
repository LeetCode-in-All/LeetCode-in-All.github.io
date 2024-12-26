[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 763\. Partition Labels

Medium

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return _a list of integers representing the size of these parts_.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"

**Output:** [9,7,8]

**Explanation:** The partition is "ababcbaca", "defegde", "hijhklij". This is a partition so that each letter appears in at most one part. A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.

**Example 2:**

**Input:** s = "eccbbbbdec"

**Output:** [10]

**Constraints:**

*   `1 <= s.length <= 500`
*   `s` consists of lowercase English letters.

## Solution

```javascript
/**
 * @param {string} s
 * @return {number[]}
 */
var partitionLabels = function(s) {
    const letters = s.split('')
    const result = []
    const position = new Array(26).fill(0)

    for (let i = 0; i < letters.length; i++) {
        position[letters[i].charCodeAt(0) - 'a'.charCodeAt(0)] = i
    }

    let prev = -1
    let max = 0

    for (let i = 0; i < letters.length; i++) {
        max = Math.max(max, position[letters[i].charCodeAt(0) - 'a'.charCodeAt(0)])
        if (i === max) {
            result.push(i - prev)
            prev = i
        }
    }

    return result
};

export { partitionLabels }
```