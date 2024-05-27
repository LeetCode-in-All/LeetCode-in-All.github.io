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

```cpp
#include <unordered_map>

class LRUCache {
private:
    struct LruCacheNode {
        int key;
        int value;
        LruCacheNode* prev;
        LruCacheNode* next;

        LruCacheNode(int k, int v) : key(k), value(v), prev(nullptr), next(nullptr) {}
    };

    int capacity;
    std::unordered_map<int, LruCacheNode*> cacheMap;
    LruCacheNode* head;
    LruCacheNode* tail;

public:
    LRUCache(int cap) : capacity(cap), head(nullptr), tail(nullptr) {}

    int get(int key) {
        auto it = cacheMap.find(key);
        if (it == cacheMap.end()) {
            return -1;
        }
        LruCacheNode* val = it->second;
        moveToHead(val);
        return val->value;
    }

    void put(int key, int value) {
        auto it = cacheMap.find(key);
        if (it != cacheMap.end()) {
            LruCacheNode* valNode = it->second;
            valNode->value = value;
            moveToHead(valNode);
        } else {
            if (cacheMap.size() < capacity) {
                LruCacheNode* node = new LruCacheNode(key, value);
                cacheMap[key] = node;
                if (head == nullptr) {
                    head = node;
                    tail = node;
                } else {
                    node->next = head;
                    head->prev = node;
                    head = node;
                }
            } else {
                // Remove from tail
                LruCacheNode* last = tail;
                tail = last->prev;
                if (tail != nullptr) {
                    tail->next = nullptr;
                }
                cacheMap.erase(last->key);
                delete last;
                if (cacheMap.size() == 0) {
                    head = nullptr;
                }
                // Call recursively
                put(key, value);
            }
        }
    }

private:
    void moveToHead(LruCacheNode* node) {
        if (node == head) {
            return;
        }
        if (node == tail) {
            tail = node->prev;
        }
        LruCacheNode* prev = node->prev;
        LruCacheNode* next = node->next;
        prev->next = next;
        if (next != nullptr) {
            next->prev = prev;
        }
        node->prev = nullptr;
        node->next = head;
        head->prev = node;
        head = node;
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```