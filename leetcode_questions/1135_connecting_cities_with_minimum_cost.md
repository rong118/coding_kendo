# 1135. Connecting Cities With Minimum Cost

## Question link
(https://leetcode.com/problems/connecting-cities-with-minimum-cost/)

## Question Description
There are N cities numbered from 1 to N.

You are given connections, where each connections[i] = [city1, city2, cost] represents the cost to connect city1 and city2 together.  (A connection is bidirectional: connecting city1 and city2 is the same as connecting city2 and city1.)

Return the minimum cost so that for every pair of cities, there exists a path of connections (possibly of length 1) that connects those two cities together.  The cost is the sum of the connection costs used. If the task is impossible, return -1.

Example 1:

> Input: N = 3, connections = [[1,2,5],[1,3,6],[2,3,1]]
>
> Output: 6
>
> Explanation: 
>
> Choosing any 2 edges will connect all cities so we choose the minimum 2.

Example 2:

> Input: N = 4, connections = [[1,2,3],[3,4,4]]
>
> Output: -1
>
> Explanation: 
>
> There is no way to connect all cities even if all edges are used.
 

Note:
- 1 <= N <= 10000
- 1 <= connections.length <= 10000
- 1 <= connections[i][0], connections[i][1] <= N
- 0 <= connections[i][2] <= 10^5
- connections[i][0] != connections[i][1]

<br/>

## 分类 && 解题思路
- graph 
- mst

## Code Implementation
```c++
// prim algorithm Elog(V)
class Solution {
public:
    int minumumCost(int N, vector<vector<int>> connections){
        unordered_map<int, vector<int>> g;
        auto comp = [] (vector<int> &a, vector<int> &b) -> bool { return a[2] < b[2]; };
        priority_queue<vector<int>, vector<vector<int>> decltype(comp) > pq (comp);
        unordered_set<int> v;
        int costs = 0;
        for(vector<int> edges : connections){ // build graph
            int x = edge[0];
            int y = edge[1];
            int cost = edge[2];
            if(g.find(x) == g.end()){ g[x] = {};}
            g[x].push_back({y, cost});

            if(g.find(y) == g.end()){ g[y] = {};}
            g[y].push_back({x, cost});
        }

        pq.push({1, 1, 0});
        while(!pq.isEmpty()){
            vector<int> cur = pq.front(); pq.pop();
            int x = cur[0], y = cur[1], cost = cur[2];
            if(v.find(y) == v.end()){
                v.insert(y);
                costs += cost;
                for(vector<int> n : g[y]){
                    pq.push({y, n[0], n[1]});
                }
            }
        }

        return v.size() == N ? costs : -1;
    }
}

// kruscal algorithm  Elog(E) E <= V
class Solution {
public:
    int minumumCost(int N, vector<vector<int>> connections){
        sort(connections.begin(), connections.end(), 
            [](const vector<int> & a, const vector<int> & b) -> bool{ 
            return a[2] < b[2]; 
        });
        DSU* dsu = new DSU(N + 1);
        int res = 0;
        int count = N;
        for(vector<int> c : connections){
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
```

## Time Complexity Analysis
Running time : Elog(V)