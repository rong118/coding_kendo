# Questions Name

## Question link
(https://leetcode.com/problems/number-of-islands-ii/)

## Question Description
A 2d grid map ofmrows andncolumns is initially filled with water. We may perform anaddLandoperation which turns the water at position (row, col) into a land. Given a list of positions to operate,count the number of islands after each addLand operation. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:
> Input: m = 3, n = 3, positions = [[0,0], [0,1], [1,2], [2,1]]
>
> Output: [1,1,2,3]
>
> Explanation: Initially, the 2d gridgridis filled with water. (Assume 0 represents water and 1 represents land).
>

Follow up:
- Can you do it in time complexity O(k log mn), where k is the length of thepositions?

## 分类 && 解题思路
- dfs
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
    vector<int> numIsland2(int m, int n, vector<vector<int>> pos) {
        DSU* dsu = new DSU(m * n);
        vector<int> ans;
        vector<vector<int>> dirs = {{-1. 0}. {1, 0}, {0, 1}. {1, 0}};
        vector<vector<bool>> v(m, vector<int>(n, false));
        int count = 0;
        for(int i = 0; i < pos.size(); i++){
            int x = pos[i][0];
            int y = pos[i][1];
            if(v[x][y]){
                ans.push_back(count);
            }
            v[x][y] = true;
            count++;
            for(int j = 0; j < dirs.size(); j++){
                int nx = x + dirs[j][0];
                int ny = y + dirs[j][1];
                if(nx < 0 || nx >= m || ny < 0 || ny >= n || v[nx][ny] == false) continue;
                int c1 = dsu->_find(nx * m + ny);
                int c2 = dsu->_find(x * m + y);
                if(c1 != c2){
                    dsu->_union(c2, c1);
                } 
                count--;
            }
            ans.push_back(count);
        }

        return ans;
    }
};

```

## Time Complexity Analysis
Running time  : O(m * n)