[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 207\. Course Schedule

Medium

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where <code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that you **must** take course <code>b<sub>i</sub></code> first if you want to take course <code>a<sub>i</sub></code>.

*   For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

**Example 1:**

**Input:** numCourses = 2, prerequisites = \[\[1,0]]

**Output:** true

**Explanation:** There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible. 

**Example 2:**

**Input:** numCourses = 2, prerequisites = \[\[1,0],[0,1]]

**Output:** false

**Explanation:** There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible. 

**Constraints:**

*   <code>1 <= numCourses <= 10<sup>5</sup></code>
*   `0 <= prerequisites.length <= 5000`
*   `prerequisites[i].length == 2`
*   <code>0 <= a<sub>i</sub>, b<sub>i</sub> < numCourses</code>
*   All the pairs prerequisites[i] are **unique**.

## Solution

```ruby
WHITE = 0
GRAY = 1
BLACK = 2

# @param {Integer} num_courses
# @param {Integer[][]} prerequisites
# @return {Boolean}
def can_finish(num_courses, prerequisites)
  adj = Array.new(num_courses) {[]}

  prerequisites.each do |pre|
    adj[pre[1]] << pre[0]
  end

  colors = Array.new(num_courses, WHITE)

  (0...num_courses).each do |i|
    if colors[i] == WHITE && !adj[i].empty? && has_cycle(adj, i, colors)
      return false
    end
  end

  true
end

private

def has_cycle(adj, node, colors)
  colors[node] = GRAY

  adj[node].each do |nei|
    return true if colors[nei] == GRAY
    return true if colors[nei] == WHITE && has_cycle(adj, nei, colors)
  end

  colors[node] = BLACK
  false
end
```