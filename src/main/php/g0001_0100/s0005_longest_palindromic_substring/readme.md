[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 5\. Longest Palindromic Substring

Medium

Given a string `s`, return _the longest palindromic substring_ in `s`.

**Example 1:**

**Input:** s = "babad"

**Output:** "bab" **Note:** "aba" is also a valid answer. 

**Example 2:**

**Input:** s = "cbbd"

**Output:** "bb" 

**Example 3:**

**Input:** s = "a"

**Output:** "a" 

**Example 4:**

**Input:** s = "ac"

**Output:** "a" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consist of only digits and English letters.

## Solution

```php
class Solution {
    /**
     * @param String $s
     * @return String
     */
    public function longestPalindrome($s): string {
        if (($length = strlen($s)) <= 1) {
            return $s;
        }
        if (strrev($s) === $s) {
            return $s;
        }

        $max_length = 1;
        for ($i = 0; $i < $length; ++$i) {
            for ($len = $max_length; $len <= $length; ++$len) {
                $start = $i - ($len >> 1);
                if ($start < 0 || $start + $len > $length) {
                    break;
                }
                $substr = substr($s, $start, $len);
                if ($substr === strrev($substr)) {
                    $str = $substr;
                    $max_length = $len;
                } elseif ($max_length + 1 < $len) {
                    break;
                }
            }
        }

        return $str;
    }
}
```