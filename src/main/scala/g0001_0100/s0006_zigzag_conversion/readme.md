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

```scala
import scala.collection.mutable

object Solution {
    def convert(s: String, numRows: Int): String = {
        if (numRows == 1) return s
        val map = new mutable.HashMap[Int, String]()
        var string = ""
        var counter = 0
        var counterBool = true
        for (i <- s) {
            val currentValue = map.getOrElse(counter, "")
            map(counter) = currentValue + i.toString
            counterBool = if (counter == numRows - 1) false else if (counter == 0) true else counterBool
            counter = if (counterBool) counter + 1 else counter - 1
        }
        map.foreach {
            case (_, value) => string += value
        }
        string
    }
}
```