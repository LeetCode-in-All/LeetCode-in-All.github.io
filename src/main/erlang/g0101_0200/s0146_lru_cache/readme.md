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

```erlang
%% Persistent Term Keys
-define(CAPACITY_KEY, {lru_cache, capacity}).
-define(CACHE_TABLE, lru_cache_cache_table).
-define(TTL_TABLE, lru_cache_ttl_table).

%% API Specifications
-spec lru_cache_init_(Capacity :: integer()) -> ok.
lru_cache_init_(Capacity) ->
    persistent_term:put(?CAPACITY_KEY, Capacity),
    case ets:info(?CACHE_TABLE) of
        undefined ->
            ets:new(?CACHE_TABLE, [set, public, named_table]),
            ets:new(?TTL_TABLE, [ordered_set, public, named_table]);
        _ ->
            ets:delete_all_objects(?CACHE_TABLE),
            ets:delete_all_objects(?TTL_TABLE)
    end,
    ok.

-spec lru_cache_get(Key :: integer()) -> integer().
lru_cache_get(Key) ->
    case extract(Key) of
        {Key, Value} ->
            insert(Key, Value),
            Value;
        -1 ->
            -1
    end.

-spec lru_cache_put(Key :: integer(), Value :: integer()) -> ok.
lru_cache_put(Key, Value) ->
    _ = extract(Key),
    insert(Key, Value),
    evict(),
    ok.

%% Internal Functions
extract(Key) ->
    case ets:lookup(?CACHE_TABLE, Key) of
        [{Key, Uniq, Value}] ->
            ets:delete(?TTL_TABLE, Uniq),
            {Key, Value};
        [] ->
            -1
    end.

insert(Key, Value) ->
    Uniq = unique_integer(),
    ets:insert(?CACHE_TABLE, {Key, Uniq, Value}),
    ets:insert(?TTL_TABLE, {Uniq, Key}).

evict() ->
    Capacity = persistent_term:get(?CAPACITY_KEY),
    CurrentSize = ets:info(?CACHE_TABLE, size),
    if
        CurrentSize > Capacity ->
            Uniq = ets:first(?TTL_TABLE),
            [{_, Key}] = ets:lookup(?TTL_TABLE, Uniq),
            ets:delete(?TTL_TABLE, Uniq),
            ets:delete(?CACHE_TABLE, Key);
        true ->
            ok
    end.

unique_integer() ->
    erlang:unique_integer([monotonic]).

%% Your functions will be called as such:
%% lru_cache_init_(Capacity),
%% Param_1 = lru_cache_get(Key),
%% lru_cache_put(Key, Value),

%% lru_cache_init_ will be called before every test case, in which you can do some necessary initializations.
```