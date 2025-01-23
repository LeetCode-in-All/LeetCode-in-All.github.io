[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 155\. Min Stack

Easy

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

*   `MinStack()` initializes the stack object.
*   `void push(int val)` pushes the element `val` onto the stack.
*   `void pop()` removes the element on the top of the stack.
*   `int top()` gets the top element of the stack.
*   `int getMin()` retrieves the minimum element in the stack.

**Example 1:**

**Input**

    ["MinStack","push","push","push","getMin","pop","top","getMin"]
    [[],[-2],[0],[-3],[],[],[],[]]

**Output:** [null,null,null,null,-3,null,0,-2]

**Explanation:**

    MinStack minStack = new MinStack();
    minStack.push(-2);
    minStack.push(0);
    minStack.push(-3);
    minStack.getMin(); // return -3
    minStack.pop();
    minStack.top(); // return 0
    minStack.getMin(); // return -2 

**Constraints:**

*   <code>-2<sup>31</sup> <= val <= 2<sup>31</sup> - 1</code>
*   Methods `pop`, `top` and `getMin` operations will always be called on **non-empty** stacks.
*   At most <code>3 * 10<sup>4</sup></code> calls will be made to `push`, `pop`, `top`, and `getMin`.

## Solution

```erlang
-spec min_stack_init_() -> any().
min_stack_init_() ->
    catch ets:delete(min_stack),
    ets:new(min_stack, [named_table, ordered_set, public]),
    ets:insert(min_stack, {size, 0}),
    ok.

-spec min_stack_push(Val :: integer()) -> any().
min_stack_push(Val) ->
    [{size, Size}] = ets:lookup(min_stack, size),
    CurrentMin = case Size of
        0 -> Val;
        _ -> min(Val, min_stack_get_min())
    end,
    ets:insert(min_stack, {Size + 1, {Val, CurrentMin}}),
    ets:insert(min_stack, {size, Size + 1}),
    ok.

-spec min_stack_pop() -> any().
min_stack_pop() ->
    [{size, Size}] = ets:lookup(min_stack, size),
    case Size > 0 of
        true ->
            ets:delete(min_stack, Size),
            ets:insert(min_stack, {size, Size - 1}),
            ok;
        false ->
            ok
    end.

-spec min_stack_top() -> integer().
min_stack_top() ->
    [{size, Size}] = ets:lookup(min_stack, size),
    case Size > 0 of
        true ->
            [{_, {Val, _}}] = ets:lookup(min_stack, Size),
            Val;
        false ->
            0  % Default value for empty stack
    end.

-spec min_stack_get_min() -> integer().
min_stack_get_min() ->
    [{size, Size}] = ets:lookup(min_stack, size),
    case Size > 0 of
        true ->
            [{_, {_, Min}}] = ets:lookup(min_stack, Size),
            Min;
        false ->
            0  % Default value for empty stack
    end.
```