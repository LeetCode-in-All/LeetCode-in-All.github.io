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

```dart
// Node class to represent each element in the stack
class Node {
  int min;
  int data;
  Node? previousNode;
  Node? nextNode;

  Node(this.min, this.data, this.previousNode, this.nextNode);
}

class MinStack {
  Node? currentNode;

  // Initialize your data structure here
  MinStack();

  // Push a value onto the stack
  void push(int val) {
    if (currentNode == null) {
      currentNode = Node(val, val, null, null);
    } else {
      currentNode!.nextNode = Node(
        (currentNode!.min < val) ? currentNode!.min : val,
        val,
        currentNode,
        null,
      );
      currentNode = currentNode!.nextNode;
    }
  }

  // Remove the element on top of the stack
  void pop() {
    if (currentNode != null) {
      currentNode = currentNode!.previousNode;
    }
  }

  // Get the top element
  int top() {
    return currentNode!.data;
  }

  // Retrieve the minimum element in the stack
  int getMin() {
    return currentNode!.min;
  }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = MinStack();
 * obj.push(val);
 * obj.pop();
 * int param3 = obj.top();
 * int param4 = obj.getMin();
 */
```