# 1192. Critical Connections in a Network

## Question link
> (https://leetcode.com/problems/critical-connections-in-a-network/)

## Question Description
There are n servers numbered from 0 to n - 1 connected by undirected server-to-server connections forming a network where connections[i] = [ai, bi] represents a connection between servers ai and bi. Any server can reach other servers directly or indirectly through the network.

A critical connection is a connection that, if removed, will make some servers unable to reach some other server.

Return all critical connections in the network in any order.

<br/>

Example 1:
>
> <img src="https://assets.leetcode.com/uploads/2019/09/03/1537_ex1_2.png" width="400" />
>
> Input: n = 4, connections = [[0,1],[1,2],[2,0],[1,3]]
>
> Output: [[1,3]]
>
> Explanation: [[3,1]] is also accepted.

Example 2:
>
> Input: n = 2, connections = [[0,1]]
>
> Output: [[0,1]]

Constraints:
- 2 <= n <= 10<sup>5</sup> 
- n - 1 <= connections.length <= 10<sup>5</sup>
- 0 <= ai, bi <= n - 1
- ai != bi
- There are no repeated connections.

## Tags
- graph
- tarjan

## Code Implementation
```c++
// tarjan O(E + V)
class Solution {
private:
    vector<vector<int> > g;
    vector<int> dfn;
    vector<int> low;
    int time;
    int n;
public:
    vector<vector<int>> criticalConnections(int n, vector<vector<int>>& connections) {
        this->n = n;
        time = 0;
        dfn.resize(n, -1);
        low.resize(n);
        vector<vector<int>> res;
        for(int i = 0; i < n; i++){
            g.push_back({});
        }
        
        for(vector<int> tmp : connections){
            g[tmp[0]].push_back(tmp[1]);
            g[tmp[1]].push_back(tmp[0]);
        }
        
        for(int i = 0; i < n; i++){
            if(dfn[i] == -1) dfs(i, i, res);
        }
        
        return res;
    }
    
    void dfs(int cur, int parent, vector<vector<int>>& res){
        dfn[cur] = low[cur] = ++time;
        for(int nei : g[cur]){
            if(nei == parent) continue; //
            if(dfn[nei] == -1){
                dfs(nei, cur, res);
                if(low[nei] > dfn[cur]) res.push_back({cur, nei});
            }
            low[cur] = min(low[cur], low[nei]);
        }
    }
};
```

## Time Complexity Analysis