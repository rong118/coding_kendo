# 261 Graph Valid Tree

## Question link
(https://leetcode.com/problems/graph-valid-tree/description/)

## Question Description
Givennnodes labeled from0ton - 1and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

For example:
Givenn = 5andedges = [[0, 1], [0, 2], [0, 3], [1, 4]], return true.
Givenn = 5andedges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]], return false.

Note: you can assume that no duplicate edges will appear inedges. Since all edges are undirected,[0, 1]is the same as[1, 0]and thus will not appear together inedges.

## Tags
- graph
- dfs
- union find

## Code Implementation
```c++
// Union Find
class DSU {
    vector<int> parent;
    DSU(int n) {
        parent.resize(n, 0);
        for(int i = 0; i < parent.size(); i++){
            parent[i] = i;
        }
    }

    int _find(int x){
        if(parent[x] != x)
            parent[x] = _find(parent[x]);
        return parent[x];
    }

    void _union(int x, int y){
        parent[find(x)] = find(y);
    }
}

class Solution {
public:
    bool validTree(int n, vector<pair<int, int>>& edges) {
        DSU* dsu = new DSU(n);
        for(auto t : edges){
            if(dsu->find(t->first) == dsu->find(t->second))
                return false;
            dsu->union(t->first, t->second);
        }

        return edges.size() == n - 1;
    }
};

// DFS with parent
class Solution {
public:
    bool validTree(int n, vector<pair<int, int>>& edges) {
        vector<vector<int>> g(n, {});
        for(int i = 0; i < edges.size(); i++){
            int s = edges[i][0];
            int t = edges[i][1];
            g[s].push_back(t);
            g[t].push_back(s);
        }

        vector<int> v(n, 0);
        if(hasCycle(g, 0, visited, -1)) return false;
        for(int i = 0; i < n; i++){
            if(!visited[i]) return false;
        }
        return true;
    }

    bool hasCycle(vector<vector<int>>& g, int s, vector<int>& v, int parent){
        v[s] = true;
        for(int i = 0; i < g[s].size(); i++){
            int t = g[s][i];
            if(!v[t]){
                if(hasCycle(g, t, v, s)) return true;
            } else{
                if(v != p) return true;
            }
        }

        return false;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)