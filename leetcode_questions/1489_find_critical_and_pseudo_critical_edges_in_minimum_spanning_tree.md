# 1489. Find Critical and Pseudo-Critical Edges in Minimum Spanning Tree

## Question link
(https://leetcode.com/problems/find-critical-and-pseudo-critical-edges-in-minimum-spanning-tree/)

## Question Description
Given a weighted undirected connected graph with n vertices numbered from 0 to n - 1, and an array edges where edges[i] = [ai, bi, weighti] represents a bidirectional and weighted edge between nodes ai and bi. A minimum spanning tree (MST) is a subset of the graph's edges that connects all vertices without cycles and with the minimum possible total edge weight.

Find all the critical and pseudo-critical edges in the given graph's minimum spanning tree (MST). An MST edge whose deletion from the graph would cause the MST weight to increase is called a critical edge. On the other hand, a pseudo-critical edge is that which can appear in some MSTs but not all.

Note that you can return the indices of the edges in any order.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/06/04/ex1.png" width="400" />
>
> Input: n = 5, edges = [[0,1,1],[1,2,1],[2,3,2],[0,3,2],[0,4,3],[3,4,3],[1,4,6]]
>
> Output: [[0,1],[2,3,4,5]]
>
> Explanation: The figure above describes the graph.
>
> The following figure shows all the possible MSTs:
>
> <img src="https://assets.leetcode.com/uploads/2020/06/04/msts.png" width="400" />
>
> Notice that the two edges 0 and 1 appear in all MSTs, therefore they are critical edges, so we return them in the first list of the output.
>
> The edges 2, 3, 4, and 5 are only part of some MSTs, therefore they are considered pseudo-critical edges. We add them to the second list of the output.

Example 2:
> <img src="https://assets.leetcode.com/uploads/2020/06/04/ex2.png" width="400" />
>
> Input: n = 4, edges = [[0,1,1],[1,2,1],[2,3,1],[0,3,1]]
>
> Output: [[],[0,1,2,3]]
>
> Explanation: We can observe that since all 4 edges have equal weight, choosing any 3 edges from the given 4 will yield an MST. Therefore all 4 edges are pseudo-critical.

<br/>

Constraints:
- 2 <= n <= 100
- 1 <= edges.length <= min(200, n * (n - 1) / 2)
- edges[i].length == 3
- 0 <= ai < bi < n
- 1 <= weighti <= 1000
- All pairs (ai, bi) are distinct.

## 分类 && 解题思路
- graph
- mst

## Code Implementation
```c++
class DSU {
    vector<int> parent;
public:
    DSU(int N){
        parent.resize(N, 0);
        for(int i = 0; i < N; i++) parent[i] = i;
    }

    int _find(int x){
        if(parent[x] != x) parent[x] = _find(parent[x]);
        return parent[x];
    }

    void _union(int x, int y){
        parent[_find(x)] = parent[_find(y)];
    }
};

class Solution {
public:
    vector<vector<int>> findCriticalAndPseudoCriticalEdges(int n, vector<vector<int>>& edges) {
        // Mark edges id
        for(int i = 0; i < edges.size(); i++){
            edges[i].push_back(i);
        }
        // Sort for kruscal algorithm
        sort(edges.begin(), edges.end(), 
            [](const vector<int> & a, const vector<int> & b) -> bool{ 
            return a[2] < b[2]; 
        });
        
        int w = _mst(n, edges, -1, -1);
        unordered_set<int> crit;
        unordered_set<int> ncrit;
        
        // Find critical
        // Disable i edge and see if mst value become larger or mst broken(-1)
        for(int i = 0; i < edges.size(); i++){
            int wr = _mst(n, edges, i, -1);
            if(wr > w || wr == -1){
                crit.insert(edges[i][3]);
            }
        }
        
        // Find non-critical
        // Link i edge in graph and see if mst value keep same
        for(int i = 0; i < edges.size(); i++){
            if(crit.find(edges[i][3]) != crit.end()) continue;
            int wr = _mst(n, edges, -1, i);
            if(wr == w){
                ncrit.insert(edges[i][3]);
            }
        }
        
        // Output
        vector<vector<int> > ans = {{}, {}};
        for(auto itr = crit.begin(); itr != crit.end(); itr++){
            ans[0].push_back(*itr);
        }
        
        for(auto itr = ncrit.begin(); itr != ncrit.end(); itr++){
            ans[1].push_back(*itr);
        }
        
        return ans;
    }
    
    // MST => kruscal algorithm
    int _mst(int N, vector<vector<int>>& connections, int disable, int link){
        DSU* dsu = new DSU(N + 1);
        int res = 0;
        int count = N;
        if(link != -1){
            vector<int> c = connections[link];
            int x = dsu->_find(c[0]);
            int y = dsu->_find(c[1]);
            dsu->_union(c[0], c[1]);
            res += c[2];
            count--;
        }

        for(int i = 0; i < connections.size(); i++){
            if(i == disable || i == link) continue;
            vector<int> c = connections[i];
            int x = dsu->_find(c[0]);
            int y = dsu->_find(c[1]);
            if(x != y){
                dsu->_union(c[0], c[1]);
                res += c[2];
                count--;
            }
        }

        return count == 1 ? res : -1;
    }
};
```

## Time Complexity Analysis