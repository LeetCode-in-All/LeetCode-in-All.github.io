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

```ruby
# @param {Character[][]} board
# @param {String} word
# @return {Boolean}
def exist(board, word)
  @row_size = board.size
  @col_size = board[0].size

  if word.match(/^#{word[0]}+/)[0].size > word.match(/#{word[-1]}+$/)[0].size
    word.reverse!
  end

  (0...board.size).each do |r|
    (0...board[0].size).each do |c|
      return true if traverse(board, word, 0, r, c)
    end
  end
  false
end

def traverse(board, word, idx, i, j)
  return false if (
  (i < 0 ||
      i >= @row_size) ||
      (j < 0 ||
          j >= @col_size) ||
      word[idx] != board[i][j]
  )
  return true if idx == word.size - 1

  board[i][j] = '#'

  res = (traverse(board, word, idx + 1, i, j + 1) ||
      traverse(board, word, idx + 1, i, j - 1) ||
      traverse(board, word, idx + 1, i + 1, j) ||
      traverse(board, word, idx + 1, i - 1, j))

  board[i][j] = word[idx]

  res
end
```