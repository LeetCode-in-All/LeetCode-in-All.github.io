[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 763\. Partition Labels

Medium

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Return _a list of integers representing the size of these parts_.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"

**Output:** [9,7,8]

**Explanation:**

    The partition is "ababcbaca", "defegde", "hijhklij".
    This is a partition so that each letter appears in at most one part.
    A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts. 

**Example 2:**

**Input:** s = "eccbbbbdec"

**Output:** [10] 

**Constraints:**

*   `1 <= s.length <= 500`
*   `s` consists of lowercase English letters.

## Solution

```cpp
#include <vector>
#include <string>
#include <unordered_map>

class Solution {
public:
    std::vector<int> partitionLabels(const std::string& s) {
        std::vector<int> result;
        std::vector<int> position(26, 0);
        
        // Store the last position of each character
        for (int i = 0; i < s.size(); ++i) {
            position[s[i] - 'a'] = i;
        }
        
        int max = 0;
        int prev = -1;
        
        for (int i = 0; i < s.size(); ++i) {
            // Update max position of current character
            if (position[s[i] - 'a'] > max) {
                max = position[s[i] - 'a'];
            }
            
            // If current index reaches max, partition found
            if (i == max) {
                result.push_back(i - prev);
                prev = i;
            }
        }
        
        return result;
    }
};
```