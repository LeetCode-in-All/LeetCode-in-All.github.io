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

```dart
class Solution {
  List<int> findAnagrams(String s, String p) {
    List<int> map = List.filled(26, 0);

    // Fill the map with the frequency of characters in string p
    for (int i = 0; i < p.length; i++) {
      map[p.codeUnitAt(i) - 'a'.codeUnitAt(0)]++;
    }

    List<int> res = [];
    int i = 0;
    int j = 0;

    while (i < s.length) {
      int idx = s.codeUnitAt(i) - 'a'.codeUnitAt(0);
      // Add the new character
      map[idx]--;

      // If the window size exceeds the length of p, remove the leftmost character
      if (i >= p.length) {
        map[s.codeUnitAt(j++) - 'a'.codeUnitAt(0)]++;
      }

      // Check if the current window is an anagram of p
      bool isAnagram = true;
      for (int k = 0; k < 26; k++) {
        if (map[k] != 0) {
          isAnagram = false;
          break;
        }
      }

      // If it is an anagram, add the start index of the window to the result
      if (i >= p.length - 1 && isAnagram) {
        res.add(j);
      }

      i++;
    }

    return res;
  }
}
```