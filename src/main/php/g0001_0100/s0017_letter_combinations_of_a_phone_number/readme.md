[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 17\. Letter Combinations of a Phone Number

Medium

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**Example 1:**

**Input:** digits = "23"

**Output:** ["ad","ae","af","bd","be","bf","cd","ce","cf"] 

**Example 2:**

**Input:** digits = ""

**Output:** [] 

**Example 3:**

**Input:** digits = "2"

**Output:** ["a","b","c"] 

**Constraints:**

*   `0 <= digits.length <= 4`
*   `digits[i]` is a digit in the range `['2', '9']`.

## Solution

```php
class Solution {
    /**
     * @param String $digits
     * @return String[]
     */
    public function letterCombinations($digits) {
        if (empty($digits)) {
            return [];
        }
        $letters = ["", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"];
        $ans = [];
        $curr = '';
        $this->findCombinations(0, $digits, $letters, $curr, $ans);
        return $ans;
    }

    private function findCombinations($start, $nums, $letters, &$curr, &$ans) {
        if (strlen($curr) == strlen($nums)) {
            $ans[] = $curr;
            return;
        }
        for ($i = $start; $i < strlen($nums); $i++) {
            $n = intval($nums[$i]);
            for ($j = 0; $j < strlen($letters[$n]); $j++) {
                $ch = $letters[$n][$j];
                $curr .= $ch;
                $this->findCombinations($i + 1, $nums, $letters, $curr, $ans);
                $curr = substr($curr, 0, -1);
            }
        }
    }
}
```