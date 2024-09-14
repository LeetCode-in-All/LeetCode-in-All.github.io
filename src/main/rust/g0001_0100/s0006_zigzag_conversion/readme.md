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

```rust
impl Solution {
    pub fn convert(s: String, num_rows: i32) -> String {
        let num_rows = num_rows as usize;
        if num_rows == 1 || s.len() < num_rows {
            return s;
        }
        
        let mut result = String::with_capacity(s.len());
        let s_bytes = s.as_bytes();
        let complete_jump = 2 * (num_rows - 1);

        for row in 0..num_rows {
            let mut index = row;
            let zig_jump = 2 * (num_rows - 1 - row);
            let zag_jump = complete_jump - zig_jump;
            let mut use_zig_jump = true;

            while index < s.len() {
                result.push(s_bytes[index] as char);
                if row == 0 || row == num_rows - 1  {
                    index += complete_jump;
                } else {
                    index += if use_zig_jump { zig_jump } else { zag_jump };
                    use_zig_jump = !use_zig_jump;
                }
            } 
        }

        result
    }
}
```