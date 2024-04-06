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

```ruby
class LRUCache
  class LruCacheNode
    attr_accessor :key, :value, :prev, :next

    def initialize(k, v)
      @key = k
      @value = v
    end
  end

=begin
    :type capacity: Integer
=end
  def initialize(cap)
    @capacity = cap
    @cache_map = {}
    # insert here
    @head = nil
    # remove here
    @tail = nil
  end

=begin
    :type key: Integer
    :rtype: Integer
=end
  def get(key)
    val_node = @cache_map[key]
    return -1 if val_node.nil?

    move_to_head(val_node)
    val_node.value
  end

=begin
    :type key: Integer
    :type value: Integer
    :rtype: Void
=end
  def put(key, value)
    val_node = @cache_map[key]

    if val_node
      val_node.value = value
      move_to_head(val_node)
    else
      if @cache_map.size < @capacity
        if @cache_map.empty?
          node = LruCacheNode.new(key, value)
          @cache_map[key] = node
          @head = node
          @tail = node
        else
          node = LruCacheNode.new(key, value)
          @cache_map[key] = node
          node.next = @head
          @head.prev = node
          @head = node
        end
      else
        # remove from tail
        last = @tail
        @tail = last.prev
        @tail.next = nil unless @tail.nil?
        @cache_map.delete(last.key)
        @head = nil if @cache_map.empty?
        # Call recursively
        put(key, value)
      end
    end
  end

  private

  def move_to_head(node)
    return if node == @head

    @tail = node.prev if node == @tail
    prev = node.prev
    nex = node.next
    prev.next = nex
    nex.prev = prev unless nex.nil?
    node.prev = nil
    node.next = @head
    @head.prev = node
    @head = node
  end
end

# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache.new(capacity)
# param_1 = obj.get(key)
# obj.put(key, value)
```