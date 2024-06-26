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

```java
public class MinStack {
    private static class Node {
        int min;
        int data;
        Node nextNode;
        Node previousNode;

        public Node(int min, int data, Node previousNode, Node nextNode) {
            this.min = min;
            this.data = data;
            this.previousNode = previousNode;
            this.nextNode = nextNode;
        }
    }

    private Node currentNode;

    // initialize your data structure here.
    public MinStack() {
        // no initialization needed.
    }

    public void push(int val) {
        if (currentNode == null) {
            currentNode = new Node(val, val, null, null);
        } else {
            currentNode.nextNode = new Node(Math.min(currentNode.min, val), val, currentNode, null);
            currentNode = currentNode.nextNode;
        }
    }

    public void pop() {
        currentNode = currentNode.previousNode;
    }

    public int top() {
        return currentNode.data;
    }

    public int getMin() {
        return currentNode.min;
    }
}

/*
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```

**Time Complexity (Big O Time):**

1. **push(int val):** The `push` operation has a time complexity of O(1). It involves creating a new node and updating pointers, both of which are constant time operations.

2. **pop():** The `pop` operation also has a time complexity of O(1). It simply involves moving the `currentNode` pointer to the previous node.

3. **top():** The `top` operation has a time complexity of O(1) because it directly accesses the `data` field of the current node.

4. **getMin():** The `getMin` operation has a time complexity of O(1) because it directly accesses the `min` field of the current node.

Overall, all the stack operations (push, pop, top, getMin) have a constant time complexity of O(1).

**Space Complexity (Big O Space):**

The space complexity of this MinStack implementation is O(N), where N is the number of elements pushed onto the stack. 

- Each element pushed onto the stack consumes space for a new node, which contains integer values (`min`, `data`), a reference to the previous node (`previousNode`), and a reference to the next node (`nextNode`).
- As you push more elements onto the stack, the memory usage increases linearly with the number of elements.

It's important to note that the space complexity is related to the number of elements in the stack (N), not the total number of operations performed. Each element added to the stack consumes additional memory.

In summary, the time complexity of all stack operations is O(1), and the space complexity is O(N), where N is the number of elements pushed onto the stack.
