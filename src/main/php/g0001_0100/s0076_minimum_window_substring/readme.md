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

```php
class Solution {
    /**
     * @param String $s
     * @param String $t
     * @return String
     */
    public function minWindow($s, $t) {
        $map = array_fill(0, 128, 0);
        for ($i = 0; $i < strlen($t); $i++) {
            $map[ord($t[$i]) - ord('A')]++;
        }
        $count = strlen($t);
        $begin = 0;
        $end = 0;
        $d = PHP_INT_MAX;
        $head = 0;
        while ($end < strlen($s)) {
            if ($map[ord($s[$end++]) - ord('A')]-- > 0) {
                $count--;
            }
            while ($count == 0) {
                if ($end - $begin < $d) {
                    $d = $end - $begin;
                    $head = $begin;
                }
                if ($map[ord($s[$begin++]) - ord('A')]++ == 0) {
                    $count++;
                }
            }
        }
        return $d == PHP_INT_MAX ? "" : substr($s, $head, $head + $d);
    }
}
```