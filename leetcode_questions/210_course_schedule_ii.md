# 210. Course Schedule II

## Question link
(https://leetcode.com/problems/course-schedule-ii/)

## Question Description
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.

<br/>

Example 1:
> Input: numCourses = 2, prerequisites = [[1,0]]
>
> Output: [0,1]
>
> Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].

Example 2:
> Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
>
> Output: [0,2,1,3]
>
> Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
>
> So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].

Example 3:
> Input: numCourses = 1, prerequisites = []
>
> Output: [0]

Constraints:
- 1 <= numCourses <= 2000
- 0 <= prerequisites.length <= numCourses * (numCourses - 1)
- prerequisites[i].length == 2
- 0 <= ai, bi < numCourses
- ai != bi
- All the pairs [ai, bi] are distinct.

## Tags
- graph
- topologic sort

## Code Implementation
```c++
// bfs
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
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

        vector<int> ans;
        int count = 0;
        // bfs put node that indegree become zero in queue and loop until queue is empty
        while(!q.empty()){
            int cur = q.front(); q.pop_front();
            count++;
            ans.push_back(cur);
            for(int neighbor : g[cur]){
                indegree[neighbor]--;
                if(indegree[neighbor] == 0){
                    q.push_back(neighbor);
                }
            }
        }

        if(count != numCourses) return {};
        
        return ans;
    }
};

// dfs 
class Solution {
    vector<vector<int> > edges;
    vector<int> visited;
    vector<int> ans;
    bool valid = true;
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        edges.resize(numCourses, {});
        visited.resize(numCourses, 0);
        for(vector<int> edge : prerequisites){
            edges[edge[1]].push_back(edge[0]);
        }

        for(int i = 0; i < numCourses; i++){
            if(visited[i] == 0){
                _dfs(i);
            }
        }

        // Return empty if there is cycle in graph
        if(!valid) return {};
        
        // reverse result due to dfs (buttom to up)
        reverse(ans.begin(), ans.end());
        return ans;
    }

    void _dfs(int u){
        visited[u] = 1;
        
        for(int v : edges[u]){
            if(visited[v] == 0) _dfs(v);
            else if(visited[v] == 1) valid = false;
        }
        ans.push_back(u);
        visited[u] = 2;
    }
};
```

## Time Complexity Analysis
Running time  : O(V + E)