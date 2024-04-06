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

```php
class Solution {
    /**
     * @param String $s
     * @return String[][]
     */
    function partition($s) {
        $res = array();
        $this->backtracking($res, array(), $s, 0);
        return $res;
    }

    private function backtracking(&$res, $currArr, $s, $start) {
        if ($start == strlen($s)) {
            array_push($res, $currArr);
        }
        for ($end = $start; $end < strlen($s); $end++) {
            if (!$this->isPanlindrome($s, $start, $end)) {
                continue;
            }
            array_push($currArr, substr($s, $start, $end - $start + 1));
            $this->backtracking($res, $currArr, $s, $end + 1);
            array_pop($currArr);
        }
    }

    private function isPanlindrome($s, $start, $end) {
        while ($start < $end && $s[$start] == $s[$end]) {
            $start++;
            $end--;
        }
        return $start >= $end;
    }
}
```