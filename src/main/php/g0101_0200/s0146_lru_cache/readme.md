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

```php
class LruCacheNode {
    public $key;
    public $value;
    public $prev;
    public $next;

    function __construct($k, $v) {
        $this->key = $k;
        $this->value = $v;
    }
}

class LRUCache {
    private $capacity;
    private $cacheMap;
    private $head;
    private $tail;

    /**
     * @param Integer $capacity
     */
    function __construct($cap) {
        $this->capacity = $cap;
        $this->cacheMap = array();
    }

    /**
     * @param Integer $key
     * @return Integer
     */
    public function get($key) {
        if (!isset($this->cacheMap[$key])) {
            return -1;
        }
        $val = $this->cacheMap[$key];
        $this->moveToHead($val);
        return $val->value;
    }

    /**
     * @param Integer $key
     * @param Integer $value
     * @return NULL
     */
    public function put($key, $value) {
        if (isset($this->cacheMap[$key])) {
            $valNode = $this->cacheMap[$key];
            $valNode->value = $value;
            $this->moveToHead($valNode);
        } else {
            if (count($this->cacheMap) < $this->capacity) {
                if (count($this->cacheMap) == 0) {
                    $node = new LruCacheNode($key, $value);
                    $this->cacheMap[$key] = $node;
                    $this->head = $node;
                    $this->tail = $node;
                } else {
                    $node = new LruCacheNode($key, $value);
                    $this->cacheMap[$key] = $node;
                    $node->next = $this->head;
                    $this->head->prev = $node;
                    $this->head = $node;
                }
            } else {
                $last = $this->tail;
                $this->tail = $last->prev;
                if ($this->tail != null) {
                    $this->tail->next = null;
                }
                unset($this->cacheMap[$last->key]);
                if (count($this->cacheMap) == 0) {
                    $this->head = null;
                }
                $this->put($key, $value);
            }
        }
    }

    private function moveToHead($node) {
        if ($node === $this->head) {
            return;
        }
        if ($node === $this->tail) {
            $this->tail = $node->prev;
        }
        $prev = $node->prev;
        $next = $node->next;
        $prev->next = $next;
        if ($next != null) {
            $next->prev = $prev;
        }
        $node->prev = null;
        $node->next = $this->head;
        $this->head->prev = $node;
        $this->head = $node;
    }
}
/**
 * Your LRUCache object will be instantiated and called as such:
 * $obj = LRUCache($capacity);
 * $ret_1 = $obj->get($key);
 * $obj->put($key, $value);
 */
```