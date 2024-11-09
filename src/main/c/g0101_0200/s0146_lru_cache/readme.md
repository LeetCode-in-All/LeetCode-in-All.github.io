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

```c
// Define a node in the doubly linked list
typedef struct LRUNode {
    int key;           // Key of the node
    int val;           // Value of the node
    struct LRUNode* prev; // Pointer to the previous node
    struct LRUNode* next; // Pointer to the next node
} LRUNode;

// Define the LRU Cache structure
typedef struct LRUCache {
    int capacity;      // Maximum number of items the cache can hold
    int size;          // Current number of items in the cache
    LRUNode* head;     // Dummy head node of the doubly linked list
    LRUNode* tail;     // Dummy tail node of the doubly linked list
    LRUNode** hash;    // Hash map to store nodes for quick access
} LRUCache;

// Create a new node
LRUNode* createNode(int key, int value) {
    LRUNode* node = (LRUNode*)malloc(sizeof(LRUNode)); // Allocate memory for the new node
    node->key = key;            // Set the key of the node
    node->val = value;          // Set the value of the node
    node->prev = NULL;          // Initialize previous pointer to NULL
    node->next = NULL;          // Initialize next pointer to NULL
    return node;                // Return the newly created node
}

// Initialize the LRU cache
LRUCache* lRUCacheCreate(int capacity) {
    LRUCache* cache = (LRUCache*)malloc(sizeof(LRUCache)); // Allocate memory for the cache
    cache->capacity = capacity;                           // Set the cache capacity
    cache->size = 0;                                     // Initialize size to 0
    cache->head = createNode(INT_MIN, INT_MIN);          // Create a dummy head node
    cache->tail = createNode(INT_MIN, INT_MIN);          // Create a dummy tail node
    cache->head->next = cache->tail;                     // Set head's next to tail
    cache->tail->prev = cache->head;                     // Set tail's prev to head
    cache->hash = (LRUNode**)calloc(10000, sizeof(LRUNode*)); // Create a hash map (size is 10000 for simplicity)

    return cache; // Return the initialized cache
}

// Remove a node from the doubly linked list
void removeNode(LRUCache* cache, LRUNode* node) {
    node->prev->next = node->next; // Bypass 'node' in the list by linking previous node to next node
    node->next->prev = node->prev; // Bypass 'node' in the list by linking next node to previous node
}

// Add a node right after the dummy head
void addNode(LRUCache* cache, LRUNode* node) {
    node->next = cache->head->next; // Set new node's next pointer to the node currently after the head
    node->prev = cache->head;       // Set new node's prev pointer to the head
    cache->head->next->prev = node; // Update the previous node's prev pointer to the new node
    cache->head->next = node;       // Update the head's next pointer to the new node
}

// Move a node to the head (most recently used)
void moveToHead(LRUCache* cache, LRUNode* node) {
    removeNode(cache, node);  // Remove node from its current position
    addNode(cache, node);    // Add node right after the head
}

// Get the value of the key if it exists
int lRUCacheGet(LRUCache* cache, int key) {
    LRUNode* node = cache->hash[key]; // Retrieve the node from the hash map using the key
    if (node == NULL) {
        return -1; // Return -1 if the key is not found
    }
    moveToHead(cache, node); // Move the accessed node to the head (most recently used)
    return node->val;        // Return the value of the node
}

// Put a key-value pair into the cache
void lRUCachePut(LRUCache* cache, int key, int value) {
    LRUNode* node = cache->hash[key]; // Retrieve the node from the hash map using the key
    if (node != NULL) {
        // If the node exists, update its value and move it to the head
        node->val = value;
        moveToHead(cache, node);
    } else {
        // If the node does not exist
        if (cache->size >= cache->capacity) {
            // If the cache is full, remove the least recently used node
            LRUNode* lru = cache->tail->prev; // The LRU node is just before the tail
            removeNode(cache, lru);           // Remove the LRU node from the list
            cache->hash[lru->key] = NULL;     // Remove the node from the hash map
            free(lru);                        // Free the memory of the removed node
            cache->size--;                    // Decrement the size of the cache
        }
        // Create a new node and add it to the cache
        LRUNode* newNode = createNode(key, value);
        addNode(cache, newNode);          // Add the new node to the head
        cache->hash[key] = newNode;       // Add the new node to the hash map
        cache->size++;                    // Increment the size of the cache
    }
}

// Free the LRU cache and all its nodes
void lRUCacheFree(LRUCache* cache) {
    LRUNode* curr = cache->head->next; // Start from the first real node
    while (curr != cache->tail) {
        LRUNode* next = curr->next; // Store the next node
        free(curr);                // Free the current node
        curr = next;               // Move to the next node
    }
    free(cache->head);   // Free the dummy head node
    free(cache->tail);   // Free the dummy tail node
    free(cache->hash);   // Free the hash map
    free(cache);         // Free the cache structure
}

/**
 * Your LRUCache struct will be instantiated and called as such:
 * LRUCache* obj = lRUCacheCreate(capacity);
 * int param_1 = lRUCacheGet(obj, key);
 * lRUCachePut(obj, key, value);
 * lRUCacheFree(obj);
 */
```