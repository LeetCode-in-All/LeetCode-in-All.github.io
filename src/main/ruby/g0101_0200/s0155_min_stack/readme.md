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

```ruby
# @param {String} string
# @return {String}
class MinStack
  class Node
    attr_accessor :min, :data, :previous_node, :next_node

    def initialize(min, data, previous_node, next_node)
      @min = min
      @data = data
      @previous_node = previous_node
      @next_node = next_node
    end
  end

  def initialize
    # no initialization needed.
  end

=begin
    :type val: Integer
    :rtype: Void
=end
  def push(val)
    if @current_node.nil?
      @current_node = Node.new(val, val, nil, nil)
    else
      @current_node.next_node = Node.new([@current_node.min, val].min, val, @current_node, nil)
      @current_node = @current_node.next_node
    end
  end

=begin
    :rtype: Integer
=end
  def pop
    @current_node = @current_node.previous_node
  end

  def top
    @current_node.data
  end

=begin
    :rtype: Integer
=end
  def get_min
    @current_node.min
  end
end

# Your MinStack object will be instantiated and called as such:
# obj = MinStack.new()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.get_min()
```