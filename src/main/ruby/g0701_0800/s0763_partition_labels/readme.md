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

```ruby
# @param {String} s
# @return {Integer[]}
def partition_labels(s)
  letters = s.chars
  result = []
  position = Array.new(26, 0)

  letters.each_with_index do |char, i|
    position[char.ord - 'a'.ord] = i
  end

  i = 0
  prev = -1
  max = 0

  while i < letters.length
    if position[letters[i].ord - 'a'.ord] > max
      max = position[letters[i].ord - 'a'.ord]
    end

    if i == max
      result.push(i - prev)
      prev = i
    end

    i += 1
  end

  result
end
```