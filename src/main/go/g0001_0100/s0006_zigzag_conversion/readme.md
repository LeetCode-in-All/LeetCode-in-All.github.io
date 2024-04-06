[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 6\. Zigzag Conversion

Medium

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P A H N A P L S I I G Y I R 

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

string convert(string s, int numRows); 

**Example 1:**

**Input:** s = "PAYPALISHIRING", numRows = 3

**Output:** "PAHNAPLSIIGYIR" 

**Example 2:**

**Input:** s = "PAYPALISHIRING", numRows = 4

**Output:** "PINALSIGYAHRPI"

**Explanation:** P I N A L S I G Y A H R P I 

**Example 3:**

**Input:** s = "A", numRows = 1

**Output:** "A" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consists of English letters (lower-case and upper-case), `','` and `'.'`.
*   `1 <= numRows <= 1000`

## Solution

```golang
func convert(s string, numRows int) string {
	topJump := (numRows-2)*2 + 2
	if topJump <= 0 {
		return s
	}
	size := len(s)
	resultArray := make([]byte, size)
	j := 0
	for i := 0; i < size; i += topJump {
		resultArray[j] = s[i]
		j++
	}
	for row := 1; row < numRows-1; row++ {
		for i := 0; i-row < size; i += topJump {
			iLeft := i - row
			iRight := i + row
			if iLeft > 0 {
				resultArray[j] = s[iLeft]
				j++
			}
			if iRight < size {
				resultArray[j] = s[iRight]
				j++
			}
		}
	}
	for i := topJump - numRows + 1; i < size; i += topJump {
		resultArray[j] = s[i]
		j++
	}
	return string(resultArray)
}
```