[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 438\. Find All Anagrams in a String

Medium

Given two strings `s` and `p`, return _an array of all the start indices of_ `p`_'s anagrams in_ `s`. You may return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** s = "cbaebabacd", p = "abc"

**Output:** [0,6]

**Explanation:** 

The substring with start index = 0 is "cba", which is an anagram of "abc". 

The substring with start index = 6 is "bac", which is an anagram of "abc".

**Example 2:**

**Input:** s = "abab", p = "ab"

**Output:** [0,1,2]

**Explanation:** 

The substring with start index = 0 is "ab", which is an anagram of "ab". 

The substring with start index = 1 is "ba", which is an anagram of "ab". 

The substring with start index = 2 is "ab", which is an anagram of "ab".

**Constraints:**

*   <code>1 <= s.length, p.length <= 3 * 10<sup>4</sup></code>
*   `s` and `p` consist of lowercase English letters.

## Solution

```javascript
/**
 * @param {string} s
 * @param {string} p
 * @return {number[]}
 */
var findAnagrams = function(s, p) {
    const map = new Array(26).fill(0)
    for (let i = 0; i < p.length; i++) {
        map[p.charCodeAt(i) - 'a'.charCodeAt(0)]++
    }

    const res = []
    let i = 0
    let j = 0

    while (i < s.length) {
        const idx = s.charCodeAt(i) - 'a'.charCodeAt(0)
        map[idx]--

        if (i >= p.length) {
            map[s.charCodeAt(j++) - 'a'.charCodeAt(0)]++
        }

        let finish = true
        for (let k = 0; k < 26; k++) {
            if (map[k] !== 0) {
                finish = false
                break
            }
        }

        if (i >= p.length - 1 && finish) {
            res.push(j)
        }
        i++
    }

    return res
};

export { findAnagrams }
```