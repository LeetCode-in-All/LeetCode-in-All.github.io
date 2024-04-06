[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 22\. Generate Parentheses

Medium

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3

**Output:** ["((()))","(()())","(())()","()(())","()()()"] 

**Example 2:**

**Input:** n = 1

**Output:** ["()"] 

**Constraints:**

*   `1 <= n <= 8`

## Solution

```php
class Solution {
    /**
     * @param Integer $n
     * @return String[]
     */
    public function generateParenthesis(int $n): array {
        $sb = '';
        $ans = [];
        return $this->generate($sb, $ans, $n, $n);
    }

    private function generate(string &$sb, array &$ans, int $open, int $close): array {
        if ($open === 0 && $close === 0) {
            $ans[] = $sb;
            return $ans;
        }
        if ($open > 0) {
            $sb .= '(';
            $this->generate($sb, $ans, $open - 1, $close);
            $sb = substr($sb, 0, -1);
        }
        if ($close > 0 && $open < $close) {
            $sb .= ')';
            $this->generate($sb, $ans, $open, $close - 1);
            $sb = substr($sb, 0, -1);
        }
        return $ans;
    }
}
```