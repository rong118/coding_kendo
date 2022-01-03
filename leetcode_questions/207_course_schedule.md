# 207 Course Schedule

## Question link
(https://leetcode.com/problems/course-schedule/)

## Question Description
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return true if you can finish all courses. Otherwise, return false.

Example 1:
> Input: numCourses = 2, prerequisites = [[1,0]]
>
> Output: true
>
> Explanation: There are a total of 2 courses to take. 
>
> To take course 1 you should have finished course 0. So it is possible.

Example 2:
> Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
>
> Output: false
>
> Explanation: There are a total of 2 courses to take. 
>
> To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
 

Constraints:
- 1 <= numCourses <= 10<sup>5</sup>
- 0 <= prerequisites.length <= 5000
- prerequisites[i].length == 2
- 0 <= ai, bi < numCourses
- All the pairs prerequisites[i] are unique.

<br/>

## 分类 && 解题思路
- graph
- topologic sort

## Code Implementation
```c++
// bfs - khan
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        // build gragh and indegree
        unordered_map<int, vector<int> > g;
        vector<int> indegree(numCourses, 0);
        for(vector<int> edge : prerequisites){
            int end = edge[0];
            int start = edge[1];
            if(g.find(start) == g.end()){
                g[start] = {};
            }
            g[start].push_back(end);
            indegree[end]++;
        }

        // find node that indegree is 0
        deque<int> q;
        for(int i = 0; i < numCourses; i++){
            if(indegree[i] == 0){
                q.push_back(i);
            }
        }

        // bfs put node that indegree become zero in queue and loop until queue is empty
        int count = 0;
        while(!q.empty()){
            int cur = q.front(); q.pop_front();
            count++;
            for(int neighbor : g[cur]){
                indegree[neighbor]--;
                if(indegree[neighbor] == 0){
                    q.push_back(neighbor);
                }
            }
        }

        // if count != numCourses == cycle find
        return count == numCourses;
    }
};

// dfs 
class Solution {
    vector<vector<int> > edges;
    vector<int> visited;
    boolean valid = true;
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        edges.resize(numCourses, {});
        visited.resize(N, 0);
        for(vector<int> edge : prerequisites){
            edges[edge[1]].push_back(edge[0]);
        }

        for(int i = 0; i < numCourses; i++){
            if(visited[i] == 0){
                _dfs(i);
            }
        }

        return valid;
    }

    void _dfs(int u){
        visited[u] = 1;
        for(int v : edges[u]){
            if(visited[v] == 0) _dfs(v);
            else if(visited[v] == 1) valid = false;
        }
        visited[u] = 2;
    }
};
```

## Time Complexity Analysis
Running time  : O(v + e)