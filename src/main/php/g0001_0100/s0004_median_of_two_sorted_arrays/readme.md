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

```php
class Solution {
    /**
     * @param Integer[] $nums1
     * @param Integer[] $nums2
     * @return Float
     */
    public function findMedianSortedArrays($nums1, $nums2) {
        $nums3 = [];
        $sum = count($nums1) + count($nums2);
        $med = ($sum / 2);
        if ($sum % 2 === 0) {
            $index = [$med - 1, $med];
        } else {
            $index = [floor($med)];
        }
        $i = 0;
        $i1 = 0;
        $i2 = 0;
        while ($i < $sum) {
            if (!isset($nums1[$i1])) {
                $nums3[] = $nums2[$i2];
                $i2++;
                $i++;
                continue;
            }
            if (!isset($nums2[$i2])) {
                $nums3[] = $nums1[$i1];
                $i1++;
                $i++;
                continue;
            }
            if ($nums1[$i1] < $nums2[$i2]) {
                $nums3[] = $nums1[$i1];
                $i1++;
            } else {
                $nums3[] = $nums2[$i2];
                $i2++;
            }
            $i++;
        }
        return isset($index[1])
            ? ($nums3[$index[0]] + $nums3[$index[1]]) / 2
            : $nums3[$index[0]];
    }
}
```