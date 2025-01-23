[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 200\. Number of Islands

Medium

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

**Input:** grid = [ 

["1","1","1","1","0"], 

["1","1","0","1","0"], 

["1","1","0","0","0"], 

["0","0","0","0","0"] 

]

**Output:** 1

**Example 2:**

**Input:** grid = [ 

["1","1","0","0","0"], 

["1","1","0","0","0"], 

["0","0","1","0","0"], 

["0","0","0","1","1"] 

]

**Output:** 3

**Constraints:**

*   `m == grid.length`
*   `n == grid[i].length`
*   `1 <= m, n <= 300`
*   `grid[i][j]` is `'0'` or `'1'`.

## Solution

```erlang
-spec num_islands([[char()]]) -> integer().
num_islands(Grid) ->
    Table = ets:new(grid, []),
    lists:foreach(
      fun({Row, I}) ->
          lists:foreach(
            fun({X, J}) when X =:= $1 ->
                ets:insert(Table, {{I, J}});
               (_) -> ok
            end,
            lists:zip(Row, lists:seq(0, length(Row) - 1))
          )
      end,
      lists:zip(Grid, lists:seq(0, length(Grid) - 1))
    ),
    count(Table, 0).

count(Table, Ans) ->
    case ets:first(Table) of
        '$end_of_table' -> Ans;
        {I, J} ->
            sink_island(Table, {I, J}),
            count(Table, Ans + 1)
    end.

sink_island(Table, {I, J}) ->
    case ets:member(Table, {I, J}) of
        true ->
            ets:delete(Table, {I, J}),
            sink_island(Table, {I - 1, J}),
            sink_island(Table, {I + 1, J}),
            sink_island(Table, {I, J - 1}),
            sink_island(Table, {I, J + 1});
        false -> ok
    end.
```