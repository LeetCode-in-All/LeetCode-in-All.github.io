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

```racket
(define lru-cache%
  (class object%
    (super-new)
    
    (init-field capacity)
    
    (define head #f)
    (define tail #f)
    (define cache (make-hash))
    
    (define/private (move-to-head node)
      (when (not (eq? node head))
        (when (eq? node tail)
          (set! tail (hash-ref node 'prev))
          (when tail (hash-set! tail 'next #f)))
        (let ((prev (hash-ref node 'prev #f))
              (next (hash-ref node 'next #f)))
          (when prev (hash-set! prev 'next next))
          (when next (hash-set! next 'prev prev))
          (hash-set! node 'prev #f)
          (hash-set! node 'next head)
          (when head (hash-set! head 'prev node))
          (set! head node))))
    
    (define/public (get key)
      (let ((node (hash-ref cache key #f)))
        (if node
            (begin (move-to-head node)
                   (hash-ref node 'value))
            -1)))
    
    (define/public (put key value)
      (let ((node (hash-ref cache key #f)))
        (if node
            (begin
              (hash-set! node 'value value)
              (move-to-head node))
            (begin
              (when (>= (hash-count cache) capacity)
                (when tail
                  (hash-remove! cache (hash-ref tail 'key))
                  (set! tail (hash-ref tail 'prev #f))
                  (when tail (hash-set! tail 'next #f))))
              (let ((new-node (make-hash)))
                (hash-set! new-node 'key key)
                (hash-set! new-node 'value value)
                (hash-set! new-node 'prev #f)
                (hash-set! new-node 'next head)
                (when head (hash-set! head 'prev new-node))
                (set! head new-node)
                (unless tail (set! tail new-node))
                (hash-set! cache key new-node))))))))
```