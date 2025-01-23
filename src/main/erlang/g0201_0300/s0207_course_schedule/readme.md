[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 207\. Course Schedule

Medium

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where <code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that you **must** take course <code>b<sub>i</sub></code> first if you want to take course <code>a<sub>i</sub></code>.

*   For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

**Example 1:**

**Input:** numCourses = 2, prerequisites = \[\[1,0]]

**Output:** true

**Explanation:** There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

**Example 2:**

**Input:** numCourses = 2, prerequisites = \[\[1,0],[0,1]]

**Output:** false

**Explanation:** There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

**Constraints:**

*   `1 <= numCourses <= 2000`
*   `0 <= prerequisites.length <= 5000`
*   `prerequisites[i].length == 2`
*   <code>0 <= a<sub>i</sub>, b<sub>i</sub> < numCourses</code>
*   All the pairs prerequisites[i] are **unique**.

## Solution

```erlang
-define(WHITE, 0).
-define(GRAY, 1).
-define(BLACK, 2).

-spec can_finish(NumCourses :: integer(), Prerequisites :: [[integer()]]) -> boolean().
can_finish(NumCourses, Prerequisites) ->
    % Create adjacency list as a list of lists instead of a map
    AdjList = create_adj_list(NumCourses, Prerequisites),
    % Use array for colors instead of map
    Colors = array:new(NumCourses, {default, ?WHITE}),
    % Check for cycles
    not has_cycle_in_graph(AdjList, Colors, 0, NumCourses).

-spec create_adj_list(NumCourses :: integer(), Prerequisites :: [[integer()]]) -> [[integer()]].
create_adj_list(NumCourses, Prerequisites) ->
    % Initialize empty lists for each course
    EmptyAdj = [[] || _ <- lists:seq(1, NumCourses)],
    % Fill adjacency lists
    lists:foldl(
        fun([To, From], Acc) ->
            lists:sublist(Acc, From) ++ 
            [[To | lists:nth(From + 1, Acc)]] ++ 
            lists:nthtail(From + 1, Acc)
        end,
        EmptyAdj,
        Prerequisites
    ).

-spec has_cycle_in_graph([[integer()]], array:array(), integer(), integer()) -> boolean().
has_cycle_in_graph(_AdjList, _Colors, Current, NumCourses) when Current >= NumCourses ->
    false;
has_cycle_in_graph(AdjList, Colors, Current, NumCourses) ->
    case array:get(Current, Colors) =:= ?WHITE andalso length(lists:nth(Current + 1, AdjList)) > 0 of
        true ->
            case dfs(AdjList, Colors, Current) of
                {true, _} -> true;
                {false, NewColors} ->
                    has_cycle_in_graph(AdjList, NewColors, Current + 1, NumCourses)
            end;
        false ->
            has_cycle_in_graph(AdjList, Colors, Current + 1, NumCourses)
    end.

-spec dfs([[integer()]], array:array(), integer()) -> {boolean(), array:array()}.
dfs(AdjList, Colors, Node) ->
    Colors1 = array:set(Node, ?GRAY, Colors),
    Neighbors = lists:nth(Node + 1, AdjList),
    check_neighbors(AdjList, Neighbors, Colors1, Node).

-spec check_neighbors([[integer()]], [integer()], array:array(), integer()) -> {boolean(), array:array()}.
check_neighbors(_, [], Colors, Node) ->
    {false, array:set(Node, ?BLACK, Colors)};
check_neighbors(AdjList, [Neighbor|Rest], Colors, Node) ->
    case array:get(Neighbor, Colors) of
        ?GRAY ->
            {true, Colors};
        ?WHITE ->
            case dfs(AdjList, Colors, Neighbor) of
                {true, NewColors} -> {true, NewColors};
                {false, NewColors} ->
                    check_neighbors(AdjList, Rest, NewColors, Node)
            end;
        ?BLACK ->
            check_neighbors(AdjList, Rest, Colors, Node)
    end.
```