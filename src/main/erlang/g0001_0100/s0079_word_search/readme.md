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

```erlang
-spec exist(Board :: [[char()]], Word :: unicode:unicode_binary()) -> boolean().

dfs_children(A,Cand,V,N,M,Next) ->
    lists:any(
        fun({I,J}) ->
            NextCh=array:get(I*M+J,A),
            V1=gb_sets:insert({I,J}, V),
            dfs(A,{NextCh,{I,J}},V1,N,M,Next)
        end, Cand).

dfs(_,_,_,_,_,[]) -> true;
dfs(A,{Ch,{I,J}},V,N,M,[Ch|[]]) -> true;
dfs(A,{Ch,{I,J}},V,N,M,[Ch|Next]) ->
    Cand=lists:filter(
        fun({I,J}) -> 
            Visited=gb_sets:is_element({I,J},V),
            (not Visited) 
             and (I>=0) 
             and (I<N) 
             and (J>=0) 
             and (J<M)
        end, [{I-1,J},{I,J-1},{I+1,J},{I,J+1}]),
    dfs_children(A,Cand,V,N,M,Next);
dfs(_,W,_,_,_,_) -> 
    false.

prefix_len([A,A|Next],Acc) -> prefix_len([A|Next],1+Acc);
prefix_len(_,Acc) -> Acc.

exist(Board, Word) ->
    A=array:from_list(lists:flatten(Board)),
    N=length(Board),
    [First|_]=Board,
    M=length(First),
    Cand=[{I,J} || I <- lists:seq(0,N-1), J <- lists:seq(0,M-1)],
    V=gb_sets:empty(),
    List=binary_to_list(Word),
    ListRev=lists:reverse(List),
    PrefixLen=prefix_len(List,1),
    SuffixLen=prefix_len(ListRev,1),
    Next = if PrefixLen < SuffixLen -> List;
              true -> ListRev
           end,
    dfs_children(A,Cand,V,N,M,Next).
```