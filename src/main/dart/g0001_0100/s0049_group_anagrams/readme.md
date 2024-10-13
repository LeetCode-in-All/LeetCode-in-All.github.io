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

```dart
class Solution {
  List<List<String>> groupAnagrams(List<String> strs) {
    Map<String, List<String>> m = {};

    if (strs.length == 1) return [strs];
    else if (strs.length == 0) return [[""]];
    else {
      for (String s in strs) {
        List<String> charList = s.split('');
        charList.sort();
        String sortedS = charList.join();

        if (m[sortedS] == null) {
          m[sortedS] = [s];
        } else {
          m[sortedS]?.add(s);
        }
      }
      return m.values.toList();
    }
  }
}
```