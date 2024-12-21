[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 239\. Sliding Window Maximum

Hard

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

**Example 1:**

**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3

**Output:** [3,3,5,5,6,7]

**Explanation:** 

Window position Max 

--------------- ----- 

[1 3 -1] -3 5 3 6 7 **3** 

1 [3 -1 -3] 5 3 6 7 **3** 

1 3 [-1 -3 5] 3 6 7 **5** 

1 3 -1 [-3 5 3] 6 7 **5** 

1 3 -1 -3 [5 3 6] 7 **6** 

1 3 -1 -3 5 [3 6 7] **7**

**Example 2:**

**Input:** nums = [1], k = 1

**Output:** [1]

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `1 <= k <= nums.length`

## Solution

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var maxSlidingWindow = function (nums, k) {
    // initialize an empty deqeue
    let dq = []
    // initailize two pointers with 0
    let i = 0, j = 0

    // intiailize an empty result variable
    let res = []

    // loop till j reaches to the end of loop
    while (j < nums.length) {

        // if dq is empty, push j
        if (dq.length === 0) {
            dq.push(j)
        } else {
            // if dq is non empty & back element in deqeue is less or equals to nums[j],
            // pop back element from deqeue
            while (dq.length !== 0 && nums[dq[dq.length - 1]] <= nums[j]) {
                dq.pop()
            }

            // push j in deqeue
            dq.push(j)
        }

        // if current window size is equals to k,
        // push front deqeue element in res
        if ((j - i + 1) === k) {
            res.push(nums[dq[0]])

            // if front deqeue element is equals to i,
            // remove front deqeue element
            if (dq[0] === i) {
                dq.shift()
            }

            // increment i by 1
            i++
        }

        // increment j by 1
        j++
    }

    // return result
    return res 
};

export { maxSlidingWindow }
```