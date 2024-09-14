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

```rust
impl Solution {
    const WHITE: i32 = 0;
    const GRAY: i32 = 1;
    const BLACK: i32 = 2;

    pub fn can_finish(num_courses: i32, prerequisites: Vec<Vec<i32>>) -> bool {
        let num_courses = num_courses as usize;
        let mut adj: Vec<Vec<i32>> = vec![vec![]; num_courses];
        let mut colors: Vec<i32> = vec![Self::WHITE; num_courses];

        for pre in prerequisites.iter() {
            adj[pre[1] as usize].push(pre[0]);
        }

        for i in 0..num_courses {
            if colors[i] == Self::WHITE && !adj[i].is_empty() {
                if Self::has_cycle(&adj, i, &mut colors) {
                    return false;
                }
            }
        }

        true
    }

    fn has_cycle(adj: &Vec<Vec<i32>>, node: usize, colors: &mut Vec<i32>) -> bool {
        colors[node] = Self::GRAY;

        for &neighbor in adj[node].iter() {
            let neighbor = neighbor as usize;
            if colors[neighbor] == Self::GRAY {
                return true;
            }
            if colors[neighbor] == Self::WHITE {
                if Self::has_cycle(adj, neighbor, colors) {
                    return true;
                }
            }
        }

        colors[node] = Self::BLACK;
        false
    }
}
```