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
*   At most 2<code> * 10<sup>5</sup></code> calls will be made to `get` and `put`.

## Solution

```scala
class LRUCache(capacity: Int) {
    case class LRUCacheNode(key: Int, var value: Int, var prev: LRUCacheNode = null, var next: LRUCacheNode = null)

    private var cacheMap: Map[Int, LRUCacheNode] = Map.empty
    private var head: LRUCacheNode = null
    private var tail: LRUCacheNode = null

    def get(key: Int): Int = {
        val node = cacheMap.get(key)
        if (node.isEmpty) {
            return -1
        }
        moveToHead(node.get)
        node.get.value
    }

    def put(key: Int, value: Int): Unit = {
        val node = cacheMap.get(key)
        if (node.isDefined) {
            node.get.value = value
            moveToHead(node.get)
        } else {
            if (cacheMap.size < capacity) {
                if (cacheMap.isEmpty) {
                    val newNode = LRUCacheNode(key, value)
                    cacheMap += (key -> newNode)
                    head = newNode
                    tail = newNode
                } else {
                    val newNode = LRUCacheNode(key, value)
                    cacheMap += (key -> newNode)
                    newNode.next = head
                    head.prev = newNode
                    head = newNode
                }
            } else {
                val last = tail
                tail = last.prev
                if (tail != null) {
                    tail.next = null
                }
                cacheMap -= last.key
                if (cacheMap.isEmpty) {
                    head = null
                }
                put(key, value)
            }
        }
    }

    private def moveToHead(node: LRUCacheNode): Unit = {
        if (node == head) {
            return
        }
        if (node == tail) {
            tail = node.prev
        }
        val prev = node.prev
        val next = node.next
        prev.next = next
        if (next != null) {
            next.prev = prev
        }
        node.prev = null
        node.next = head
        head.prev = node
        head = node
    }
}
```