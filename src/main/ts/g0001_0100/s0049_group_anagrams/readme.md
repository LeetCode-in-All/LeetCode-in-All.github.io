[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 49\. Group Anagrams

Medium

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** strs = ["eat","tea","tan","ate","nat","bat"]

**Output:** [["bat"],["nat","tan"],["ate","eat","tea"]] 

**Example 2:**

**Input:** strs = [""]

**Output:** [[""]] 

**Example 3:**

**Input:** strs = ["a"]

**Output:** [["a"]] 

**Constraints:**

*   <code>1 <= strs.length <= 10<sup>4</sup></code>
*   `0 <= strs[i].length <= 100`
*   `strs[i]` consists of lowercase English letters.

## Solution

```typescript
function groupAnagrams(strs: string[]): string[][] {
    if (strs.length === 1) return [strs]
    const map = new Map()
    function getKey(str: string): string {
        const charCount = Array(26).fill(0)
        for (const char of str) {
            charCount[char.charCodeAt(0) - 'a'.charCodeAt(0)]++
        }
        return charCount.join('#')
    }
    for (const str of strs) {
        const key = getKey(str)
        if (map.has(key)) {
            map.get(key).push(str)
        } else {
            map.set(key, [str])
        }
    }
    return Array.from(map.values())
}

export { groupAnagrams }
```