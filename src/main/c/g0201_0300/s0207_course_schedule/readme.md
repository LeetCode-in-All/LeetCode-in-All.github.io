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

```c
typedef struct node {
    int V;
    struct node* next;
} node;

bool dfs(node** adjlist, bool* visited, bool* recStack, int current);

bool canFinish(int numCourses, int** prerequisites, int prerequisitesSize, int* prerequisitesColSize) {
    node** adjlist = malloc(sizeof(node*) * numCourses);
    for (int i = 0; i < numCourses; i++) {
        adjlist[i] = NULL;
    }
    for (int i = 0; i < prerequisitesSize; i++) {
        node* Node = malloc(sizeof(node));
        Node->V = prerequisites[i][0];
        Node->next = adjlist[prerequisites[i][1]];
        adjlist[prerequisites[i][1]] = Node;
    }

    bool* visited = calloc(sizeof(bool), numCourses);
    bool* recStack = calloc(sizeof(bool), numCourses);

    for (int V = 0; V < numCourses; V++) {
        if (dfs(adjlist, visited, recStack, V)) {
            return false;
        }
    }
    return true;
}

bool dfs(node** adjlist, bool* visited, bool* recStack, int current) {
    if (recStack[current]) {
        return true;
    }
    if (visited[current]) {
        return false;
    }
    visited[current] = true;
    recStack[current] = true;

    for (node* Node = adjlist[current]; Node; Node = Node->next) {
        if (dfs(adjlist, visited, recStack, Node->V)) {
            return true;
        }
    }

    recStack[current] = false;
    return false;
}
```