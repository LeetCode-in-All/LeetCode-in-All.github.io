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

```php
class Node {
    public $min;
    public $data;
    public $nextNode;
    public $previousNode;

    function __construct($min, $data, $previousNode, $nextNode) {
        $this->min = $min;
        $this->data = $data;
        $this->previousNode = $previousNode;
        $this->nextNode = $nextNode;
    }
}

class MinStack {
    private $currentNode;

    function __construct() {
        // no initialization needed.
    }

    /**
     * @param Integer $val
     * @return NULL
     */
    public function push($val) {
        if ($this->currentNode == null) {
            $this->currentNode = new Node($val, $val, null, null);
        } else {
            $this->currentNode->nextNode = new Node(min($this->currentNode->min, $val), $val, $this->currentNode, null);
            $this->currentNode = $this->currentNode->nextNode;
        }
    }

    /**
     * @return NULL
     */
    public function pop() {
        $this->currentNode = $this->currentNode->previousNode;
    }

    /**
     * @return Integer
     */
    public function top() {
        return $this->currentNode->data;
    }

    /**
     * @return Integer
     */
    function getMin() {
        return $this->currentNode->min;
    }
}
```