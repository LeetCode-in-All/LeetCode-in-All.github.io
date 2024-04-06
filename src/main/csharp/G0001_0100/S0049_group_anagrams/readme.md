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

```csharp
public class Solution {
    public IList<IList<string>> GroupAnagrams(string[] strs) {
        var map = new Dictionary<string, IList<string>>();
        // allocate memory only once and reuse it to sort the chars of each s in strs.
        var buffer = new char[10000];
        var bufferSpan = new Span<char>(buffer);
        foreach (var s in strs) {
            s.CopyTo(bufferSpan);
            Array.Sort(buffer, 0, s.Length);
            var key = new string(buffer, 0, s.Length);
            if (!map.TryGetValue(key, out var value)) {
                map[key] = value = new List<string>();
            }
            value.Add(s);
        }
        return map.Values.Cast<IList<string>>().ToList();
    }
}
```