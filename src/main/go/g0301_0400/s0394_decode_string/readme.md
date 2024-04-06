[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 394\. Decode String

Medium

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed <code>10<sup>5</sup></code>.

**Example 1:**

**Input:** s = "3[a]2[bc]"

**Output:** "aaabcbc"

**Example 2:**

**Input:** s = "3[a2[c]]"

**Output:** "accaccacc"

**Example 3:**

**Input:** s = "2[abc]3[cd]ef"

**Output:** "abcabccdcdcdef"

**Constraints:**

*   `1 <= s.length <= 30`
*   `s` consists of lowercase English letters, digits, and square brackets `'[]'`.
*   `s` is guaranteed to be **a valid** input.
*   All the integers in `s` are in the range `[1, 300]`.

## Solution

```golang
import (
	"strings"
)

type Decoder struct {
	s string
	i int
}

func (d *Decoder) decodeString(s string) string {
	d.s = s
	return d.decode()
}

func (d *Decoder) decode() string {
	count := 0
	var sb strings.Builder

	for d.i < len(d.s) {
		c := d.s[d.i]
		d.i++

		if isLetter(c) {
			sb.WriteByte(c)
		} else if isDigit(c) {
			count = count*10 + int(c-'0')
		} else if c == ']' {
			break
		} else if c == '[' {
			// subproblem
			repeat := d.decode()
			for count > 0 {
				sb.WriteString(repeat)
				count--
			}
		}
	}

	return sb.String()
}

func isLetter(c byte) bool {
	return (c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z')
}

func isDigit(c byte) bool {
	return c >= '0' && c <= '9'
}

func decodeString(s string) string {
	d := Decoder{}
	return d.decodeString(s)
}
```