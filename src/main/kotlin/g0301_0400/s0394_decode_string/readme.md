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

```kotlin
class Solution {
    private var i = 0

    fun decodeString(s: String): String {
        var count = 0
        val sb = StringBuilder()
        while (i < s.length) {
            val c = s[i]
            i++
            if (Character.isLetter(c)) {
                sb.append(c)
            } else if (Character.isDigit(c)) {
                count = count * 10 + Character.getNumericValue(c)
            } else if (c == ']') {
                break
            } else if (c == '[') {
                // sub problem
                val repeat = decodeString(s)
                while (count > 0) {
                    sb.append(repeat)
                    count--
                }
            }
        }
        return sb.toString()
    }
}
```