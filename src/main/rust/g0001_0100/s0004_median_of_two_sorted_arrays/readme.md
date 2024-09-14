[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 4\. Median of Two Sorted Arrays

Hard

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

**Example 1:**

**Input:** nums1 = [1,3], nums2 = [2]

**Output:** 2.00000

**Explanation:** merged array = [1,2,3] and median is 2. 

**Example 2:**

**Input:** nums1 = [1,2], nums2 = [3,4]

**Output:** 2.50000

**Explanation:** merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5. 

**Example 3:**

**Input:** nums1 = [0,0], nums2 = [0,0]

**Output:** 0.00000 

**Example 4:**

**Input:** nums1 = [], nums2 = [1]

**Output:** 1.00000 

**Example 5:**

**Input:** nums1 = [2], nums2 = []

**Output:** 2.00000 

**Constraints:**

*   `nums1.length == m`
*   `nums2.length == n`
*   `0 <= m <= 1000`
*   `0 <= n <= 1000`
*   `1 <= m + n <= 2000`
*   <code>-10<sup>6</sup> <= nums1[i], nums2[i] <= 10<sup>6</sup></code>

## Solution

```rust
impl Solution {
    pub fn find_median_sorted_arrays(nums1: Vec<i32>, nums2: Vec<i32>) -> f64 {
        let (nums1, nums2) = if nums1.len() > nums2.len() {
            // Ensures nums1 is the smaller array
            (nums2, nums1)
        } else {
            (nums1, nums2)
        };
        
        let n1 = nums1.len();
        let n2 = nums2.len();
        let mut low = 0;
        let mut high = n1;

        while low <= high {
            let cut1 = (low + high) / 2;
            let cut2 = (n1 + n2 + 1) / 2 - cut1;

            let l1 = if cut1 == 0 { i32::MIN } else { nums1[cut1 - 1] };
            let l2 = if cut2 == 0 { i32::MIN } else { nums2[cut2 - 1] };
            let r1 = if cut1 == n1 { i32::MAX } else { nums1[cut1] };
            let r2 = if cut2 == n2 { i32::MAX } else { nums2[cut2] };

            if l1 <= r2 && l2 <= r1 {
                // Found the correct partition
                if (n1 + n2) % 2 == 0 {
                    return (f64::from(l1.max(l2)) + f64::from(r1.min(r2))) / 2.0;
                } else {
                    return f64::from(l1.max(l2));
                }
            } else if l1 > r2 {
                high = cut1 - 1;
            } else {
                low = cut1 + 1;
            }
        }

        // Fallback case, should never hit
        0.0
    }
}
```