[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 6\. Zigzag Conversion

Medium

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P A H N A P L S I I G Y I R 

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

string convert(string s, int numRows); 

**Example 1:**

**Input:** s = "PAYPALISHIRING", numRows = 3

**Output:** "PAHNAPLSIIGYIR" 

**Example 2:**

**Input:** s = "PAYPALISHIRING", numRows = 4

**Output:** "PINALSIGYAHRPI"

**Explanation:** P I N A L S I G Y A H R P I 

**Example 3:**

**Input:** s = "A", numRows = 1

**Output:** "A" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consists of English letters (lower-case and upper-case), `','` and `'.'`.
*   `1 <= numRows <= 1000`

## Solution

```erlang
%% Define the function specification
-spec convert(S :: unicode:unicode_binary(), NumRows :: integer()) -> unicode:unicode_binary().
convert(S, NumRows) ->
    %% Convert the input string to a list of characters
    CharList = unicode:characters_to_list(S),
    Length = length(CharList),
    %% Handle edge cases
    if
        NumRows == 1; NumRows >= Length ->
            S;
        true ->
            %% Initialize a list of empty lists (rows) with length NumRows
            Rows = lists:map(fun(_) -> [] end, lists:seq(1, NumRows)),
            %% Build the zigzag pattern
            ZigzagRows = build_zigzag(CharList, Rows, 0, true),
            %% Concatenate all rows to form the result
            unicode:characters_to_binary(lists:append(ZigzagRows))
    end.

%% Recursive function to build zigzag rows
-spec build_zigzag([integer()], [[integer()]], integer(), boolean()) -> [[integer()]].
build_zigzag([], Rows, _, _) ->
    Rows;
build_zigzag([Char | Rest], Rows, CurrentRow, GoingDown) ->
    %% Add the character to the current row
    UpdatedRows = update_row(Rows, CurrentRow, Char),
    %% Determine the new direction and row index
    {NewDirection, NewRow} = case {CurrentRow, GoingDown} of
        {0, _} -> {true, 1};
        {Row, _} when Row == length(Rows) - 1 -> {false, Row - 1};
        {Row, true} -> {true, Row + 1};
        {Row, false} -> {false, Row - 1}
    end,
    %% Recursively build the zigzag pattern
    build_zigzag(Rest, UpdatedRows, NewRow, NewDirection).

%% Helper function to update the row with the new character
-spec update_row([[integer()]], integer(), integer()) -> [[integer()]].
update_row(Rows, Index, Char) ->
    lists:sublist(Rows, Index) ++ [lists:nth(Index + 1, Rows) ++ [Char]] ++ lists:nthtail(Index + 1, Rows).
```