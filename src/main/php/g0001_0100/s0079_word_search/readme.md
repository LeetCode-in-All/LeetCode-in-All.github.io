[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 79\. Word Search

Medium

Given an `m x n` grid of characters `board` and a string `word`, return `true` _if_ `word` _exists in the grid_.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

**Input:** board = \[\["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"

**Output:** true 

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

**Input:** board = \[\["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"

**Output:** true 

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

**Input:** board = \[\["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"

**Output:** false 

**Constraints:**

*   `m == board.length`
*   `n = board[i].length`
*   `1 <= m, n <= 6`
*   `1 <= word.length <= 15`
*   `board` and `word` consists of only lowercase and uppercase English letters.

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?

## Solution

```php
class Solution {
    /**
     * @param String[][] $board
     * @param String $word
     * @return Boolean
     */
    public function exist($board, $word) {
        $wordCountMap = [];
        for ($i = 0; $i < strlen($word); $i++) {
            $char = $word[$i];
            if (isset($wordCountMap[$char])) {
                $wordCountMap[$char] += 1;
            } else {
                $wordCountMap[$char] = 1;
            }
        }
        $positions = [];
        foreach ($board as $rowIdx => $items) {
            foreach ($items as $colIdx => $item) {
                if ($item === $word[0]) {
                    $positions[] = [$rowIdx, $colIdx];
                }
                if (isset($wordCountMap[$item])) {
                    $wordCountMap[$item]--;
                }
            }
        }
        foreach ($wordCountMap as $count) {
            if ($count > 0) {
                return false;
            }
        }
        foreach ($positions as $position) {
            if ($this->dfs($board, $word, 0, $position)) {
                return true;
            }
        }
        return false;
    }

    function dfs($board, $word, $index, $position) {
        [$x, $y] = $position;
        if (!isset($board[$x][$y])) {
            return false;
        }
        if ($board[$x][$y] !== $word[$index]) {
            return false;
        } elseif ($index === strlen($word) - 1) {
            return true;
        }
        $board[$x][$y] = '-1';
        $dirs = [[0, 1], [0, -1], [1, 0], [-1, 0]];
        foreach ($dirs as $dir) {
            $newX = $x + $dir[0];
            $newY = $y + $dir[1];
            if ($this->dfs($board, $word, $index + 1, [$newX, $newY])) {
                return true;
            }
        }
        return false;
    }
}
```