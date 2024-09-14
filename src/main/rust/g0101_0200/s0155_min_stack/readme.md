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

```rust
pub struct MinStack {
    current_node: Option<Box<Node>>,
}

/**
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
struct Node {
    min: i32,
    data: i32,
    next_node: Option<Box<Node>>,
    previous_node: Option<Box<Node>>,
}

impl Node {
    fn new(min: i32, data: i32, previous_node: Option<Box<Node>>, next_node: Option<Box<Node>>) -> Self {
        Node {
            min,
            data,
            next_node,
            previous_node,
        }
    }
}

impl MinStack {
    pub fn new() -> Self {
        MinStack { current_node: None }
    }

    pub fn push(&mut self, val: i32) {
        match &self.current_node {
            None => {
                self.current_node = Some(Box::new(Node::new(val, val, None, None)));
            }
            Some(current) => {
                let min = std::cmp::min(current.min, val);
                let previous_node = self.current_node.take();
                self.current_node = Some(Box::new(Node::new(min, val, previous_node, None)));
            }
        }
    }

    pub fn pop(&mut self) {
        if let Some(current) = self.current_node.take() {
            self.current_node = current.previous_node;
        }
    }

    pub fn top(&self) -> i32 {
        if let Some(current) = &self.current_node {
            return current.data;
        }
        panic!("Stack is empty!");
    }

    pub fn get_min(&self) -> i32 {
        if let Some(current) = &self.current_node {
            return current.min;
        }
        panic!("Stack is empty!");
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * let obj = MinStack::new();
 * obj.push(val);
 * obj.pop();
 * let ret_3: i32 = obj.top();
 * let ret_4: i32 = obj.get_min();
 */
```