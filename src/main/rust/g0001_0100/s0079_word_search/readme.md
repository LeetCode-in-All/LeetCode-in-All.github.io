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

```rust
impl Solution {
    pub fn exist(mut board: Vec<Vec<char>>, word: String) -> bool {
        let mut word = Vec::from_iter(word.chars());
        let mut map = [0; 58]; //A-65 z-122
        for i in 0..board.len() {
            for j in 0..board[0].len() {
                map[(board[i][j] as u8 - 65) as usize] += 1;
            }
        }

        for c in &word {
            if map[(*c as u8 - 65) as usize] == 0 {
                return false;
            }
        }

        if map[(word[0] as u8 - 65) as usize] > map[(word[word.len() - 1] as u8 - 65) as usize] {
            word.reverse();
        }

        for i in 0..board.len() {
            for j in 0..board[0].len() {
                if board[i][j] != word[0] {
                    continue;
                }
                let mut p = 0;
                let (mut k, mut l) = (i, j);
                let mut dir = vec![-1; word.len() - 1];
                loop {
                    if p == word.len() - 1 {
                        return true;
                    }
                    if dir[p] == -1 {
                        board[k][l] = ' ';
                        dir[p] = 0;
                        if k > 0 && board[k - 1][l] == word[p + 1] {
                            p += 1;
                            k -= 1;
                            continue;
                        }
                    }
                    if dir[p] == 0 {
                        dir[p] = 1;
                        if l < board[k].len() - 1 && board[k][l + 1] == word[p + 1] {
                            p += 1;
                            l += 1;
                            continue;
                        }
                    }
                    if dir[p] == 1 {
                        dir[p] = 2;
                        if k < board.len() - 1 && board[k + 1][l] == word[p + 1] {
                            p += 1;
                            k += 1;
                            continue;
                        }
                    }
                    if dir[p] == 2 {
                        dir[p] = 3;
                        if l > 0 && board[k][l - 1] == word[p + 1] {
                            p += 1;
                            l -= 1;
                            continue;
                        }
                    }
                    while p > 0 && dir[p] == 3 {
                        board[k][l] = word[p];
                        dir[p] = -1;
                        p -= 1;
                        if dir[p] == 0 {
                            k += 1;
                            continue;
                        }
                        if dir[p] == 1 {
                            l -= 1;
                            continue;
                        }
                        if dir[p] == 2 {
                            k -= 1;
                            continue;
                        }
                        if dir[p] == 3 {
                            l += 1;
                            continue;
                        }
                    }
                    if p == 0 && dir[p] == 3 {
                        board[k][l] = word[p];
                        break;
                    }
                }
            }
        }
        false
    }
}
```