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

```golang
type State int

const (
	Unvisited State = iota
	Visiting
	Visited
)

func canFinish(numCourses int, prerequisites [][]int) bool {
	visited := make([]State, numCourses)
	graph := make([][]int, numCourses)
	for _, dep := range prerequisites {
		graph[dep[1]] = append(graph[dep[1]], dep[0])
	}
	for i := 0; i < numCourses; i++ {
		if visited[i] == Unvisited {
			if !dfs(i, visited, graph) {
				return false
			}
		}
	}
	return true
}

func dfs(start int, visited []State, graph [][]int) bool {
	if visited[start] == Visiting {
		return false
	}
	if visited[start] == Visited {
		return true
	}
	visited[start] = Visiting
	for _, next := range graph[start] {
		if !dfs(next, visited, graph) {
			return false
		}
	}
	visited[start] = Visited
	return true
}
```