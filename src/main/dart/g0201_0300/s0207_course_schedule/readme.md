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

*   `1 <= numCourses <= 2000`
*   `0 <= prerequisites.length <= 5000`
*   `prerequisites[i].length == 2`
*   <code>0 <= a<sub>i</sub>, b<sub>i</sub> < numCourses</code>
*   All the pairs prerequisites[i] are **unique**.

## Solution

```dart
class Solution {
  static const int WHITE = 0;
  static const int GRAY = 1;
  static const int BLACK = 2;

  bool canFinish(int numCourses, List<List<int>> prerequisites) {
    List<List<int>> adj = List.generate(numCourses, (_) => []);

    for (var pre in prerequisites) {
      adj[pre[1]].add(pre[0]);
    }

    List<int> colors = List.filled(numCourses, WHITE);

    for (int i = 0; i < numCourses; i++) {
      if (colors[i] == WHITE && adj[i].isNotEmpty && _hasCycle(adj, i, colors)) {
        return false;
      }
    }
    return true;
  }

  bool _hasCycle(List<List<int>> adj, int node, List<int> colors) {
    colors[node] = GRAY;

    for (int nei in adj[node]) {
      if (colors[nei] == GRAY) {
        return true;
      }
      if (colors[nei] == WHITE && _hasCycle(adj, nei, colors)) {
        return true;
      }
    }
    colors[node] = BLACK;
    return false;
  }
}
```