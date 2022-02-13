# 1168. Optimize Water Distribution in a Village

## Question link
> (https://leetcode.com/problems/optimize-water-distribution-in-a-village/)

## Question Description
There are n houses in a village. We want to supply water for all the houses by building wells and laying pipes.

For each house i, we can either build a well inside it directly with cost wells[i], or pipe in water from another well to it. The costs to lay pipes between houses are given by the array pipes, where each pipes[i] = [house1, house2, cost] represents the cost to connect house1 and house2 together using a pipe. Connections are bidirectional.

Find the minimum total cost to supply water to all houses.

Example 1:
> <img src="https://camo.githubusercontent.com/2ede13124d2b65792127b24b9772f16378198a3a58ee5e62b242e4fcafaac53a/68747470733a2f2f747661312e73696e61696d672e636e2f6c617267652f30303753385a496c6c793167686c74796d6f6370676a33306369306263337a302e6a7067" width="400" />
>
> Input: n = 3, wells = [1,2,2], pipes = [[1,2,1],[2,3,1]]
> 
> Output: 3

> Explanation: 
> The image shows the costs of connecting houses using pipes.
> The best strategy is to build a well in the first house with cost 1 and connect the other houses to it with cost 2 so the total cost is 3.

Constraints:
- 1 <= n <= 10000
- wells.length == n
- 0 <= wells[i] <= 10^<sup>5</sup> 
- 1 <= pipes.length <= 10000
- 1 <= pipes[i][0], pipes[i][1] <= n
- 0 <= pipes[i][2] <= 10^<sup>5</sup> 
- pipes[i][0] != pipes[i][1]

<br/>

## 分类 && 解题思路
- graph
- mst

## Code Implementation
```c++
class Solution {
public:
    int minCostToSupplyWater(int n, vector<int> wells, vector<vector<int>> pipes){
        unordered_map<int, unordered_map<int, int>> g;
        for(int i = 1; i <= n; i++){
            if(g.find(i) == g.end()){
                unordered_map<int, int> tmp;
                g[i] = tmp;
            }
            g[0][i] = wells[i - 1];
        }

        // 建图 c++ default value in map ???
        for(int i = 0; i < pipes.size(); i++){
            vector<int> edge = pipes[i]; 
            if(g.find(edge[0]) == g.end()){
                unordered_map<int, int> tmp;
                g[edge[0]] = tmp;
            }
            if(g[edge[0]].find(edge[1]) == g[edge[0]].end()){
                g[edge[0]][edge[1] = INT_MAX;
            }
            int minFrom0To1 = g[edge[0]][edge[1];
            g[edge[0]][edge[1]] = min(edge[2], minFrom0To1);

            if(g.find(edge[1]) == g.end()){
                unordered_map<int, int> tmp;
                g[edge[1]] = tmp;
            }
            if(g[edge[1]].find(edge[0]) == g[edge[1]].end()){
                g[edge[1]][edge[0] = INT_MAX;
            }

            int minFrom1To0 = g[edge[1]][edge[0];
            g[edge[1]][edge[0] = min(edge[2], minFrom1To0);
        }
        
        int res = 0;
        auto comp = [] (vector<int> &a, vector<int> &b) -> bool { return a[1] < b[1]; };
        priority_queue<vector<int>, vector<vector<int>> decltype(comp) > pq (comp);
        unordered_set<int> v;
        pq.push({0, 0});
        while(!pq.isEmpty()){
            vector<int> cur = pq.front(); pq.pop();
            int curNode = cur[0], dis = cur[2];
            if(v.find(curNode) != v.end()) continue;

            v.insert(curNode);
            res += dis;
            for(auto itr = g[curNode].begin(); itr != g[curNode].end(); itr++){
                int nei = itr->first;
                if(v.find(nei) == v.end()){
                    pq.push({nei, g[curNode][nei]});
                }
            }
        }

        return res;
    }
}


```

## Time Complexity Analysis
Running time  : O(Elog(v))