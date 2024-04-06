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

```scala
import scala.collection.mutable.ArrayBuffer

object Solution {
    val WHITE = 0
    val GRAY = 1
    val BLACK = 2

    def canFinish(numCourses: Int, prerequisites: Array[Array[Int]]): Boolean = {
        val adj = Array.fill(numCourses)(new ArrayBuffer[Int]())
        prerequisites.foreach { pre =>
            adj(pre(1)).append(pre(0))
        }

        val colors = Array.fill(numCourses)(WHITE)
        (0 until numCourses).forall { i =>
            if (colors(i) == WHITE && adj(i).nonEmpty && hasCycle(adj, i, colors)) {
                false
            } else {
                true
            }
        }
    }

    private def hasCycle(adj: Array[ArrayBuffer[Int]], node: Int, colors: Array[Int]): Boolean = {
        colors(node) = GRAY
        adj(node).foreach { nei =>
            if (colors(nei) == GRAY) {
                return true
            }
            if (colors(nei) == WHITE && hasCycle(adj, nei, colors)) {
                return true
            }
        }
        colors(node) = BLACK
        false
    }
}
```