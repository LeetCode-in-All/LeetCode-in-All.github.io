[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 74\. Search a 2D Matrix

Medium

Write an efficient algorithm that searches for a value `target` in an `m x n` integer matrix `matrix`. This matrix has the following properties:

*   Integers in each row are sorted from left to right.
*   The first integer of each row is greater than the last integer of the previous row.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

**Input:** matrix = \[\[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3

**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

**Input:** matrix = \[\[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13

**Output:** false

**Constraints:**

*   `m == matrix.length`
*   `n == matrix[i].length`
*   `1 <= m, n <= 100`
*   <code>-10<sup>4</sup> <= matrix[i][j], target <= 10<sup>4</sup></code>

## Solution

```erlang
-spec search_matrix(Matrix :: [[integer()]], Target :: integer()) -> boolean().
search_matrix(Matrix, Target) -> 
    % Get the total number of rows and columns
    {Rows, Cols} = {length(Matrix), length(hd(Matrix))},
    
    % Perform binary search
    binary_search(Matrix, Rows, Cols, Target, 0, Rows * Cols - 1).

% Function to perform binary search
-spec binary_search([[integer()]], integer(), integer(), integer(), integer(), integer()) -> boolean().
binary_search(Matrix, Rows, Cols, Target, Left, Right) ->
    if 
        Left > Right -> 
            false; % If left index exceeds the right one, return false
        true ->
            % Calculate mid index and get corresponding row and column
            Mid = (Left + Right) div 2,
            {Row, Col} = {Mid div Cols, Mid rem Cols},
            
            % Fetch the value from the matrix
            Value = lists:nth(Col + 1, lists:nth(Row + 1, Matrix)),
            
            % If the value equals the target, return true
            if
                Value == Target -> 
                    true;
                Value < Target -> 
                    % If the value is less than the target, search in the right half
                    binary_search(Matrix, Rows, Cols, Target, Mid + 1, Right);
                true -> 
                    % If the value is greater than the target, search in the left half
                    binary_search(Matrix, Rows, Cols, Target, Left, Mid - 1)
            end
    end.
```