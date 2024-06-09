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
object Solution {
    def canFinish(numCourses: Int, prerequisites: Array[Array[Int]]): Boolean = {
        import scala.collection.mutable.{Queue, ListBuffer}
        val indegree = Array.fill(numCourses)(0)
        val graph = Array.fill(numCourses)(new ListBuffer[Int])
        for (data <- prerequisites) {
            val course = data.head
            val prerequisiteCourse = data.last
            indegree(course) = indegree(course) + 1
            graph(prerequisiteCourse) += course
        }
        val startingCourses = indegree.zipWithIndex.filter(_._1.equals(0)).map(_._2)
        val queue = Queue[Int](startingCourses: _*)
        var courseTaken = 0
        while (queue.nonEmpty) {
            val current = queue.dequeue
            courseTaken = courseTaken + 1
            for (neighbor <- graph(current)) {
                indegree(neighbor) = indegree(neighbor) - 1
                if (indegree(neighbor).equals(0)) {
                    queue.enqueue(neighbor)
                }
            }
        }
        courseTaken == numCourses
    }
}
```