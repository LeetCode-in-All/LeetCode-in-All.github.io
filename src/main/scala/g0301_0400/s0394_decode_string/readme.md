[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 394\. Decode String

Medium

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there won't be input like `3a` or `2[4]`.

**Example 1:**

**Input:** s = "3[a]2[bc]"

**Output:** "aaabcbc" 

**Example 2:**

**Input:** s = "3[a2[c]]"

**Output:** "accaccacc" 

**Example 3:**

**Input:** s = "2[abc]3[cd]ef"

**Output:** "abcabccdcdcdef" 

**Example 4:**

**Input:** s = "abc3[cd]xyz"

**Output:** "abccdcdcdxyz" 

**Constraints:**

*   `1 <= s.length <= 30`
*   `s` consists of lowercase English letters, digits, and square brackets `'[]'`.
*   `s` is guaranteed to be **a valid** input.
*   All the integers in `s` are in the range `[1, 300]`.

## Solution

```scala
object Solution {
    def decodeString(s: String): String = {
        val brStack = scala.collection.mutable.Stack[Int]()
        val stStack = scala.collection.mutable.Stack[String]()
        stStack.push("")
        var i = 0
        while (i < s.length) {
            if (s(i) - '0' <= 9) {
                var j = ""
                while (s(i) != '[') {
                    j += s(i)
                    i += 1
                }
                brStack.push(j.toInt)
                stStack.push("")
            } else if (s(i) == ']') {
                val o = brStack.pop()
                val o1 = stStack.pop()
                var r = ""
                for (_ <- 0 until o) r += o1
                stStack.push(stStack.pop() + r)
            } else {
                stStack.push(stStack.pop() + s(i))
            }
            i += 1
        }
        stStack.pop()
    }
}
```