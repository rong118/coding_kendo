# 1584. Min Cost to Connect All Points

## Question link
> (https://leetcode.com/problems/min-cost-to-connect-all-points/)

## Question Description
You are given an array points representing integer coordinates of some points on a 2D-plane, where points[i] = [xi, yi].

The cost of connecting two points [xi, yi] and [xj, yj] is the manhattan distance between them: |xi - xj| + |yi - yj|, where |val| denotes the absolute value of val.

Return the minimum cost to make all points connected. All points are connected if there is exactly one simple path between any two points.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/08/26/d.png" width="400" />
>
> Input: points = [[0,0],[2,2],[3,10],[5,2],[7,0]]
> 
> Output: 20
> 
> Explanation:
> 
> <img src="https://assets.leetcode.com/uploads/2020/08/26/c.png" width="400" />
>
> We can connect the points as shown above to get the minimum cost of 20.
>
> Notice that there is a unique path between every pair of points.

Example 2:
> Input: points = [[3,12],[-2,5],[-4,1]]
>
> Output: 18
>

Constraints:
- 1 <= points.length <= 1000
- -10<sup>6</sup> <= xi, yi <= 10<sup>6</sup>
- All pairs (xi, yi) are distinct.

## Tags
- graph
- mst

## Code Implementation
```c++
// (MST) Prim native
class Solution {
public:
    int minCostConnectPoints(vector<vector<int>>& points) {
        int n = points.size();
        vector<vector<int> > mat(n, vector<int>(n, 0));
        for(int i = 0; i < n; i ++){
            for(int j =0; j < n; j++){
                mat[i][j] = abs(points[i][0] - points[j][0]) +
                        abs(points[i][1] - points[j][1]);
            }
        }
        vector<bool> visited(n, false);
        vector<int> dis(n, INT_MAX);
        dis[0] = 0;
        for(int i =0; i < n; i++){
            int nextClose = -1;
            for(int j = 0; j < n; j++)
                if(!visited[j] && (nextClose == -1 || dis[j] < dis[nextClose])) nextClose = j;
            visited[nextClose] = true;
            for(int y = 0; y < n; y++){
                if(!visited[y]) dis[y] = min(dis[y], mat[nextClose][y]);
            }
        }
        
        return accumulate(dis.begin(), dis.end(), 0);
    }
};
```

## Time Complexity Analysis
Running time  : O(V^2)