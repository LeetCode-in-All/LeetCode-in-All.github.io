[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 560\. Subarray Sum Equals K

Medium

Given an array of integers `nums` and an integer `k`, return _the total number of subarrays whose sum equals to_ `k`.

A subarray is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**

**Input:** nums = [1,1,1], k = 2

**Output:** 2

**Example 2:**

**Input:** nums = [1,2,3], k = 3

**Output:** 2

**Constraints:**

*   <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
*   `-1000 <= nums[i] <= 1000`
*   <code>-10<sup>7</sup> <= k <= 10<sup>7</sup></code>

## Solution

```c
typedef struct Node {
    int val;
    int count;
    struct Node *next;
} Node;

int hash(int val) {
    return (val + 1000001) % 10007;
}

void insert(Node **ht, int val) {
    Node *n;
    int bucket = hash(val);
    if (ht[bucket] != NULL) {
        n = ht[bucket];
        while (n != NULL) {
            if (n->val == val) {
                ++n->count;
                return;
            } else {
                n = n->next;
            }
        }
    }
    n = malloc(sizeof(Node));
    n->val = val;
    n->count = 1;
    n->next = ht[bucket];
    ht[bucket] = n;
}

int occurrences(Node **ht, int val) {
    int bucket = hash(val);
    Node *n = ht[bucket];
    while(n != NULL) {
        if (n->val == val) {
            return n->count;
        }
        n = n->next;
    }
    return 0;
}

int subarraySum(int* nums, int numsSize, int k){
    int i, count, currentCount;
    Node *hashTable[10007] = {NULL};
    count = nums[0] == k;
    insert(hashTable, nums[0]);
    for (i = 1; i < numsSize; ++i) {
        nums[i] += nums[i-1];
        if (nums[i] == k) {
            ++count;
        }
        count += occurrences(hashTable, nums[i]-k);
        insert(hashTable, nums[i]);
    }
    return count;
}
```