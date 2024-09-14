[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 146\. LRU Cache

Medium

Design a data structure that follows the constraints of a **[Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU)**.

Implement the `LRUCache` class:

*   `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
*   `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
*   `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

**Example 1:**

**Input** ["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"] [[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]

**Output:** [null, null, null, 1, null, -1, null, -1, 3, 4]

**Explanation:** 

LRUCache lRUCache = new LRUCache(2); 

lRUCache.put(1, 1); // cache is {1=1} 

lRUCache.put(2, 2); // cache is {1=1, 2=2} 

lRUCache.get(1); // return 1 

lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3} 

lRUCache.get(2); // returns -1 (not found) 

lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}

lRUCache.get(1); // return -1 (not found) 

lRUCache.get(3); // return 3 

lRUCache.get(4); // return 4

**Constraints:**

*   `1 <= capacity <= 3000`
*   <code>0 <= key <= 10<sup>4</sup></code>
*   <code>0 <= value <= 10<sup>5</sup></code>
*   At most <code>2 * 10<sup>5</sup></code> calls will be made to `get` and `put`.

## Solution

```rust
struct LRUCache {
    map: HashMap<i32, Rc<RefCell<Node>>>,
    list: LinkedList,
    size: i32,
    capacity: i32,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
use std::cell::RefCell;
use std::collections::HashMap;
use std::rc::Rc;

struct Node {
    key: i32,
    value: i32,
    prev: Option<Rc<RefCell<Node>>>,
    next: Option<Rc<RefCell<Node>>>,
}

#[derive(Default)]
struct LinkedList {
    head: Option<Rc<RefCell<Node>>>,
    tail: Option<Rc<RefCell<Node>>>,
}

impl LinkedList {
    fn new() -> LinkedList {
        Default::default()
    }

    fn move_to_head(&mut self, node: &Rc<RefCell<Node>>) {
        let prev = node.borrow().prev.as_ref().map(|a| Rc::clone(a));
        let next = node.borrow().next.as_ref().map(|a| Rc::clone(a));
        match (&prev, &next) {
            (None, None) => {
                // this is the only node in list, so do nothng
            }
            (Some(_), None) => {
                // this node is already the head, so do nothing
            }
            (None, Some(next)) => {
                // this is the tail, move it to front
                node.borrow_mut().next = None;
                node.borrow_mut().prev = None;
                next.borrow_mut().prev = None;
                self.tail = Some(Rc::clone(next));

                let prev_head = self.head.as_ref().unwrap();
                prev_head.borrow_mut().next = Some(Rc::clone(node));
                node.borrow_mut().prev = Some(Rc::clone(prev_head));
                self.head = Some(Rc::clone(node));
            }
            (Some(prev), Some(next)) => {
                node.borrow_mut().next = None;
                node.borrow_mut().prev = None;

                prev.borrow_mut().next = Some(Rc::clone(next));
                next.borrow_mut().prev = Some(Rc::clone(prev));

                let prev_head = self.head.as_ref().unwrap();
                prev_head.borrow_mut().next = Some(Rc::clone(node));
                node.borrow_mut().prev = Some(Rc::clone(prev_head));
                self.head = Some(Rc::clone(node));
            }
        }
    }

    fn push_front(&mut self, node: &Rc<RefCell<Node>>) {
        match &self.head {
            None => {
                self.head = Some(Rc::clone(node));
                self.tail = Some(Rc::clone(node));
            }
            Some(prev_head) => {
                Rc::clone(node).borrow_mut().prev = Some(Rc::clone(prev_head));
                prev_head.borrow_mut().next = Some(Rc::clone(node));
                self.head = Some(Rc::clone(node));
            }
        }
    }

    fn remove_tail(&mut self) -> Option<Rc<RefCell<Node>>> {
        if let Some(tail) = self.tail.as_ref().map(|a| a.clone()) {
            if let Some(tail_next) = tail.borrow().next.as_ref() {
                tail_next.borrow_mut().prev = None;
                self.tail = Some(Rc::clone(tail_next));
            }
            tail.borrow_mut().next = None;
            tail.borrow_mut().prev = None;
            return Some(tail);
        }
        None
    }
}

impl LRUCache {
    fn new(capacity: i32) -> Self {
        Self {
            map: HashMap::new(),
            list: LinkedList::new(),
            size: 0,
            capacity,
        }
    }

    fn get(&mut self, key: i32) -> i32 {
        if let Some(node) = self.map.get(&key) {
            self.list.move_to_head(node);
            return node.borrow().value;
        } else {
            return -1;
        }
    }

    fn put(&mut self, key: i32, value: i32) {
        if let Some(node) = self.map.get(&key) {
            self.list.move_to_head(node);
            node.borrow_mut().value = value;
        } else {
            // remove tail node if needed
            if self.size >= self.capacity {
                if let Some(prev_tail) = self.list.remove_tail() {
                    self.map.remove(&prev_tail.borrow().key);
                };
            }
            // add node to list head
            let node = Rc::new(RefCell::new(Node {
                prev: None,
                next: None,
                key,
                value,
            }));
            self.list.push_front(&node);
            // update hashmap
            self.map.insert(key, node);
            // update size
            self.size += 1;
        }
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * let obj = LRUCache::new(capacity);
 * let ret_1: i32 = obj.get(key);
 * obj.put(key, value);
 */
```