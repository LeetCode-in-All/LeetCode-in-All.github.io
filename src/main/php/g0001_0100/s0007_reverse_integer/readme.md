[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 7\. Reverse Integer

Medium

Given a signed 32-bit integer `x`, return `x` _with its digits reversed_. If reversing `x` causes the value to go outside the signed 32-bit integer range <code>[-2<sup>31</sup>, 2<sup>31</sup> - 1]</code>, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

**Example 1:**

**Input:** x = 123

**Output:** 321 

**Example 2:**

**Input:** x = -123

**Output:** -321 

**Example 3:**

**Input:** x = 120

**Output:** 21 

**Example 4:**

**Input:** x = 0

**Output:** 0 

**Constraints:**

*   <code>-2<sup>31</sup> <= x <= 2<sup>31</sup> - 1</code>

## Solution

```php
class Solution {
    /**
     * @param Integer $x
     * @return Integer
     */
    public function reverse($x) {
        $ls_negative = '';
        if (strpos($x, '-') === 0) {
            $ls_negative = substr($x, 0, 1);
            $x = substr($x, 1);
        }
        $la_chars = str_split($x);
        $la_chars = array_reverse($la_chars);
        $li_result = intval($ls_negative . implode('', $la_chars));
        if ($li_result > 2147483647 || $li_result < -2147483647) {
            $li_result = 0;
        }
        return $li_result;
    }
}
```