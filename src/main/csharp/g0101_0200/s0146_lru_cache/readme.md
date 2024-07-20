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

```csharp
public class LRUCache {
    private readonly int capacity;
    private readonly Dictionary<int, LinkedListNode<CacheItem>> cacheMap;
    private readonly LinkedList<CacheItem> cacheList;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        cacheMap = new Dictionary<int, LinkedListNode<CacheItem>>(capacity);
        cacheList = new LinkedList<CacheItem>();
    }
    
    public int Get(int key) {
        if (cacheMap.TryGetValue(key, out var node)) {
            cacheList.Remove(node);
            cacheList.AddFirst(node);
            return node.Value.Value;
        }
        return -1;
    }
    
    public void Put(int key, int value) {
        if (cacheMap.TryGetValue(key, out var node)) {
            node.Value.Value = value;
            cacheList.Remove(node);
            cacheList.AddFirst(node);
        } else {
            if (cacheMap.Count >= capacity) {
                var lastNode = cacheList.Last;
                cacheMap.Remove(lastNode.Value.Key);
                cacheList.RemoveLast();
            }
            var newNode = new LinkedListNode<CacheItem>(new CacheItem(key, value));
            cacheMap.Add(key, newNode);
            cacheList.AddFirst(newNode);
        }
    }

    private class CacheItem {
        public int Key { get; }
        public int Value { get; set; }

        public CacheItem(int key, int value) {
            Key = key;
            Value = value;
        }
    }
}

public class KeyNode {
    private int _key;
    private int _val;
    private KeyNode _next;

    public int key { 
        get { return _key; }
        set { _key = value; } 
    }

    public int val {
        get { return _val; }
        set { _val = value; }
    }

    public KeyNode next {
        get { return _next; }
        set { _next = value; }
    }

    public KeyNode() {
        _key = int.MinValue;
        _val = int.MinValue;
        _next = null;
    }

    public KeyNode(int key, int val): this() {
        _key = key;
        _val = val;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.Get(key);
 * obj.Put(key,value);
}
```