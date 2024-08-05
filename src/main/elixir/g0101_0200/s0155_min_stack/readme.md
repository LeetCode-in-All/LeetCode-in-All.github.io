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

```elixir
defmodule MinStack do
  use GenServer
  
  @spec init_() :: any
  def init_() do
    GenServer.start_link(__MODULE__, nil, [name: __MODULE__])
    GenServer.call(__MODULE__, :init)
  end

  @spec push(val :: integer) :: any
  def push(val) do
    GenServer.call(__MODULE__, {:push, val})
  end

  @spec pop() :: any
  def pop() do
    GenServer.call(__MODULE__, :pop)
  end

  @spec top() :: integer
  def top() do
    GenServer.call(__MODULE__, :top)
  end

  @spec get_min() :: integer
  def get_min() do
    GenServer.call(__MODULE__, :min)
  end

  @impl true
  def init() do
    {:ok, nil}
  end

  @impl true
  def handle_call(:init, _, _) do
    {:reply, nil, []}
  end
  
  def handle_call({:push, val}, _, []) do
    {:reply, nil, [{val, val}]}
  end
  def handle_call({:push, val}, _, [{x, m} | tail]) do
    {:reply, nil, [{val, min(val, m)}, {x, m} | tail]}
  end

  def handle_call(:pop, _, [_ | tail]) do
    {:reply, nil, tail}
  end

  def handle_call(:top, _, list = [{x, _} | _]) do
    {:reply, x, list}
  end

  def handle_call(:min, _, list = [{_, m} | _]) do
    {:reply, m, list}
  end
end

# Your functions will be called as such:
# MinStack.init_()
# MinStack.push(val)
# MinStack.pop()
# param_3 = MinStack.top()
# param_4 = MinStack.get_min()

# MinStack.init_ will be called before every test case, in which you can do some necessary initializations.
```