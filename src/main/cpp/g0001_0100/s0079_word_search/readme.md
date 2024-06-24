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

```cpp
#include <vector>

class Solution {
    static constexpr char TOMBSTONE = '#';
    
    const vector<pair<int, int>> adj_deltas = {
        {1, 0}, {-1, 0}, {0, 1}, {0, -1}
    };
    
    bool is_valid(const vector<vector<char>>& board, int r, int c) {
        return r >= 0 && r < board.size() && c >= 0 && c < board[0].size() && board[r][c] != TOMBSTONE;
    }
    
    bool dfs(vector<vector<char>>& board, string_view w, int r, int c) {
        if (w.empty() || (w.size() == 1 && w[0] == board[r][c])) {
            return true;
        }
        if (w[0] != board[r][c]) {
            return false;
        }
        bool res = false;
        board[r][c] = TOMBSTONE;
        for (auto& d : adj_deltas) {
            if (int rr = r + d.first, cc = c + d.second; is_valid(board, rr, cc)) {
                res |= dfs(board, w.substr(1), rr, cc);
            }
        }
        board[r][c] = w[0];
        return res;
    }
    
public:
    bool exist(vector<vector<char>>& board, string_view word) {
        // pruning #1
        // board has enough letters for word
        if (board.size() * board[0].size() < word.size()) {
            return false;
        }
        // pruning #2
        // all letters in word exist on board
        unordered_map<char, int> board_freq;
        for (int r = 0; r < board.size(); r++) {
            for (int c = 0; c < board[0].size(); c++) {
                board_freq[board[r][c]]++;
            }
        }
        unordered_map<char, int> word_freq;
        for (char ch : word) {
            if (++word_freq[ch] > board_freq[ch]) {
                return false;
            }
        }
        // pruning #3
        // all adjacent letters in word exist on board
        // it can be merged with pruning #2, but it's still faster than 100%
        unordered_map<char, unordered_set<char>> adj_letters;
        for (char ch : word) {
            adj_letters[ch] = {};
        }
        for (int r = 0; r < board.size(); r++) {
            for (int c = 0; c < board[0].size(); c++) {
                if (!adj_letters.count(board[r][c])) {
                    continue;
                }
                auto& st = adj_letters[board[r][c]];
                for (auto& d : adj_deltas) {
                    if (int rr = r + d.first, cc = c + d.second; is_valid(board, rr, cc)) {
                        st.insert(board[rr][cc]);
                    }
                }
            }
        }
        for (int i = 0; i < word.size(); i++) {
            if (i > 0 && adj_letters[word[i]].count(word[i - 1]) == 0) {
                return false;
            }
            if (i + 1 < word.size() && adj_letters[word[i]].count(word[i + 1]) == 0) {
                return false;
            }
        }
        // full dfs scan otherwise
        for (int r = 0; r < board.size(); r++) {
            for (int c = 0; c < board[0].size(); c++) {
                if (dfs(board, word, r, c)) {
                    return true;
                }
            }
        }
        return false;
    }
};
```