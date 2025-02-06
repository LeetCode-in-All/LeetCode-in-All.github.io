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

```racket
(define/contract (exist board word)
  (-> (listof (listof char?)) string? boolean?)
  (let* ([rows (length board)]
         [cols (length (first board))]
         [word-len (string-length word)])
    
    (define (dfs board x y index)
      (if (= index word-len)
          #t
          (let ([current (list-ref (list-ref board x) y)]
                [next-char (string-ref word index)])
            (define directions '((-1 0) (1 0) (0 -1) (0 1)))  ; up down left right
            (define new-board 
              (list-set board x 
                        (list-set (list-ref board x) y #\-)))
            
            (ormap
             (λ (dir)
               (let ([new-x (+ x (first dir))]
                     [new-y (+ y (second dir))])
                 (and (>= new-x 0) (< new-x rows)
                      (>= new-y 0) (< new-y cols)
                      (char=? (list-ref (list-ref board new-x) new-y) next-char)
                      (dfs new-board new-x new-y (add1 index)))))
             directions))))
    
    (for*/or ([i (range rows)]
              [j (range cols)])
      (and (char=? (list-ref (list-ref board i) j) 
                   (string-ref word 0))
           (dfs board i j 1)))))
```