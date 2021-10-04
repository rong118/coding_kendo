# 547 Number of Provinces

## Question link
(https://leetcode.com/problems/number-of-provinces/)

## Question Description
There are n cities. Some of them are connected, while some are not. If city a is connected directly with city b, and city b is connected directly with city c, then city a is connected indirectly with city c.
A province is a group of directly or indirectly connected cities and no other cities outside of the group.
You are given an n x n matrix isConnected where isConnected[i][j] = 1 if the i<sup>th</sup> city and the jth city are directly connected, and isConnected[i][j] = 0 otherwise.

Return the total number of provinces.

Example 1:
> ![Image](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)
>
> Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]
>
> Output: 2

Example 2:
> ![Image](https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg)
>
> Input: isConnected = [[1,0,0],[0,1,0],[0,0,1]]
>
> Output: 3

Constraints:
- 1 <= n <= 200
- n == isConnected.length
- n == isConnected[i].length
- isConnected[i][j] is 1 or 0.
- isConnected[i][i] == 1
- isConnected[i][j] == isConnected[j][i]

## 分类 && 解题思路
- graph
- unionfind

## Code Implementation
```c++
class DSU {
public:
    vector<int> parent;
    DSU(int N){
        parent.resize(N);
        for(int i = 0; i < N; i++){
            parent[i] = i;
        }
    }

    int _find(int x){
        if(parent[x] != x)
            parent[x] = _find(parent[x]);
        
        return parent[x];
    }

    void _union(int x, int y){
        parent[_find(x)] = _find(y);
        return; 
    }
};

class Solution {
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        DSU* dsu = new DSU(isConnected.size());
        
        for(int i = 0; i < isConnected.size(); i++){
            for(int j = 0; j < isConnected[i].size(); j++){
                if(isConnected[i][j] == 1){
                    dsu->_union(i, j);
                }
            }
        }

        int ans = 0;
        for(int i = 0; i < isConnected.size(); i++){
            if(dsu->_find(i) == i){
                ans++;
            }
        }

        return ans;
    }
};
```

## Time Complexity Analysis
Running time  : O(N * N * log*N)