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

```swift
class MinStack {
    private class Node {
        var min: Int
        var data: Int
        var nextNode: Node?
        var previousNode: Node?
        
        init(_ min: Int, _ data: Int, _ previousNode: Node?, _ nextNode: Node?) {
            self.min = min
            self.data = data
            self.previousNode = previousNode
            self.nextNode = nextNode
        }
    }
    
    private var currentNode: Node?
    
    init() {}
    
    func push(_ val: Int) {
        if currentNode == nil {
            currentNode = Node(val, val, nil, nil)
        } else {
            let newNode = Node(min(currentNode!.min, val), val, currentNode, nil)
            currentNode!.nextNode = newNode
            currentNode = newNode
        }
    }
    
    func pop() {
        currentNode = currentNode?.previousNode
    }
    
    func top() -> Int {
        return currentNode!.data
    }
    
    func getMin() -> Int {
        return currentNode!.min
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * let obj = MinStack()
 * obj.push(val)
 * obj.pop()
 * let ret_3: Int = obj.top()
 * let ret_4: Int = obj.getMin()
 */
```