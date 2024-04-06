[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 76\. Minimum Window Substring

Hard

Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window substring** of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window. If there is no such substring__, return the empty string_ `""`_._

The testcases will be generated such that the answer is **unique**.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "ADOBECODEBANC", t = "ABC"

**Output:** "BANC"

**Explanation:** The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t. 

**Example 2:**

**Input:** s = "a", t = "a"

**Output:** "a"

**Explanation:** The entire string s is the minimum window. 

**Example 3:**

**Input:** s = "a", t = "aa"

**Output:** ""

**Explanation:** Both 'a's from t must be included in the window. Since the largest window of s only has one 'a', return empty string. 

**Constraints:**

*   `m == s.length`
*   `n == t.length`
*   <code>1 <= m, n <= 10<sup>5</sup></code>
*   `s` and `t` consist of uppercase and lowercase English letters.

**Follow up:** Could you find an algorithm that runs in `O(m + n)` time?

## Solution

```scala
object Solution {
    def minWindow(s: String, t: String): String = {
        val map = new Array[Int](128)
        t.foreach(char => map(char - 'A') += 1)

        var count = t.length
        var begin = 0
        var end = 0
        var d = Int.MaxValue
        var head = 0

        while (end < s.length) {
            if (map(s.charAt(end) - 'A') > 0) {
                count -= 1
            }
            map(s.charAt(end) - 'A') -= 1
            end += 1

            while (count == 0) {
                if (end - begin < d) {
                    d = end - begin
                    head = begin
                }
                if (map(s.charAt(begin) - 'A') == 0) {
                    count += 1
                }
                map(s.charAt(begin) - 'A') += 1
                begin += 1
            }
        }

        if (d == Int.MaxValue) "" else s.substring(head, head + d)
    }
}
```