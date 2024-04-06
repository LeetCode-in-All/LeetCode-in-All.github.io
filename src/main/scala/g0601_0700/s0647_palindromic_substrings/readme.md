[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 647\. Palindromic Substrings

Medium

Given a string `s`, return _the number of **palindromic substrings** in it_.

A string is a **palindrome** when it reads the same backward as forward.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "abc"

**Output:** 3

**Explanation:** Three palindromic strings: "a", "b", "c". 

**Example 2:**

**Input:** s = "aaa"

**Output:** 6

**Explanation:** Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa". 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consists of lowercase English letters.

## Solution

```scala
object Solution {
    private def expand(a: Array[Char], l: Int, r: Int, res: Array[Int]): Unit = {
        var left = l
        var right = r
        while (left >= 0 && right < a.length) {
            if (a(left) != a(right)) {
                return
            } else {
                res(0) += 1
                left -= 1
                right += 1
            }
        }
    }

    def countSubstrings(s: String): Int = {
        val a = s.toCharArray
        val res = Array(0)
        for (i <- 0 until a.length) {
            expand(a, i, i, res)
            expand(a, i, i + 1, res)
        }
        res(0)
    }
}
```