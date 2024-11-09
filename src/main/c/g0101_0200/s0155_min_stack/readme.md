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

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

// Define the structure for a node in the stack
typedef struct Node {
    int min;
    int data;
    struct Node* nextNode;
    struct Node* previousNode;
} Node;

// Define the structure for MinStack
typedef struct {
    Node* currentNode;
} MinStack;

// Function to create a new node
Node* createNode(int min, int data, Node* previousNode, Node* nextNode) {
    Node* node = (Node*)malloc(sizeof(Node));
    node->min = min;
    node->data = data;
    node->previousNode = previousNode;
    node->nextNode = nextNode;
    return node;
}

// Initialize MinStack
MinStack* minStackCreate() {
    MinStack* stack = (MinStack*)malloc(sizeof(MinStack));
    stack->currentNode = NULL;
    return stack;
}

// Push a value onto the MinStack
void minStackPush(MinStack* obj, int val) {
    if (obj->currentNode == NULL) {
        obj->currentNode = createNode(val, val, NULL, NULL);
    } else {
        obj->currentNode->nextNode = createNode(
            (val < obj->currentNode->min) ? val : obj->currentNode->min, 
            val, 
            obj->currentNode, 
            NULL
        );
        obj->currentNode = obj->currentNode->nextNode;
    }
}

// Pop the top element from the MinStack
void minStackPop(MinStack* obj) {
    if (obj->currentNode != NULL) {
        Node* temp = obj->currentNode;
        obj->currentNode = obj->currentNode->previousNode;
        free(temp);
    }
}

// Get the top element of the MinStack
int minStackTop(MinStack* obj) {
    if (obj->currentNode != NULL) {
        return obj->currentNode->data;
    }
    return INT_MIN; // Or an error code if stack is empty
}

// Get the minimum element in the MinStack
int minStackGetMin(MinStack* obj) {
    if (obj->currentNode != NULL) {
        return obj->currentNode->min;
    }
    return INT_MIN; // Or an error code if stack is empty
}

// Free the MinStack
void minStackFree(MinStack* obj) {
    while (obj->currentNode != NULL) {
        minStackPop(obj);
    }
    free(obj);
}

/**
 * Your MinStack struct will be instantiated and called as such:
 * MinStack* obj = minStackCreate();
 * minStackPush(obj, val);
 
 * minStackPop(obj);
 
 * int param_3 = minStackTop(obj);
 
 * int param_4 = minStackGetMin(obj);
 
 * minStackFree(obj);
*/
```