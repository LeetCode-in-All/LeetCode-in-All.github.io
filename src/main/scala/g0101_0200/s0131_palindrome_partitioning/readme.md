[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 131\. Palindrome Partitioning

Medium

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

**Example 1:**

**Input:** s = "aab"

**Output:** [["a","a","b"],["aa","b"]] 

**Example 2:**

**Input:** s = "a"

**Output:** [["a"]] 

**Constraints:**

*   `1 <= s.length <= 16`
*   `s` contains only lowercase English letters.

## Solution

```scala
object Solution {
    def partition(s: String): List[List[String]] = {
        val res = scala.collection.mutable.ListBuffer[List[String]]()
        backtracking(res, List.empty[String], s, 0)
        res.toList
    }

    private def backtracking(res: scala.collection.mutable.ListBuffer[List[String]], currArr: List[String], s: String, start: Int): Unit = {
        if (start == s.length) {
            res += currArr.reverse
        }
        for (end <- start until s.length) {
            if (isPalindrome(s, start, end)) {
                backtracking(res, s.substring(start, end + 1) :: currArr, s, end + 1)
            }
        }
    }

    private def isPalindrome(s: String, start: Int, end: Int): Boolean = {
        var left = start
        var right = end
        while (left < right && s(left) == s(right)) {
            left += 1
            right -= 1
        }
        left >= right
    }
}
```