# 787. Cheapest Flights Within K Stops

## Question link
> (https://leetcode.com/problems/cheapest-flights-within-k-stops/)

## Question Description
There are n cities connected by some number of flights. You are given an array flights where flights[i] = [fromi, toi, pricei] indicates that there is a flight from city fromi to city toi with cost pricei.

You are also given three integers src, dst, and k, return the cheapest price from src to dst with at most k stops. If there is no such route, return -1.

Example 1:
> <img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/02/16/995.png" width="400" />
>
> Input: n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 1
>
> Output: 200
>
> Explanation: The graph is shown.
>
> The cheapest price from city 0 to city 2 with at most 1 stop costs 200, as marked red in the picture.


Example 2:
> <img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/02/16/995.png" width="400" />
>
> Input: n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 0
> 
> Output: 500
>
> Explanation: The graph is shown.
>
> The cheapest price from city 0 to city 2 with at most 0 stop costs 500, as marked blue in the picture.

Constraints:
- 1 <= n <= 100
- 0 <= flights.length <= (n * (n - 1) / 2)
- flights[i].length == 3
- 0 <= fromi, toi < n
- fromi != toi
- 1 <= pricei <= 104
- There will not be any multiple flights between two cities.
- 0 <= src, dst, k < n
- src != dst

## Tags
- graph 
- dijkstra
- bellman-ford

## Code Implementation
```c++
// dijkstra
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        vector<pair<int,int>> adj[n];
        for(const auto &x : flights){
            adj[x[0]].push_back({x[1], x[2]});
        }
        set<vector<int>> q;  // TLE if use priority_queue 
        q.insert({0,src,k});
        while(q.size() > 0){
            auto x = *q.begin(); q.erase(q.begin());
            int cost = x[0], node = x[1], stops = x[2];
            if(node == dst)return cost;
            if(stops >= 0){
                for(auto &y : adj[node]){
                    q.insert({y.second + cost, y.first, stops-1});
                }
            }
        }
        return -1;
    }
};

// bellman-ford
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        const int max = 1000000000;
        vector<int> cost(n, max);
        cost[src] = 0;
        int res = max;
        for(int i = 0; i <= k; i++){
            vector<int> cur = cost;
            for(vector<int> flight : flights){
                cur[flight[1]] = min(cur[flight[1]], cost[flight[0]] + flight[2]);
            }
            res = min(res, cur[dst]);
            cost = cur;
        }

        return res == max ? -1 : res;
    }
};

```
## Time Complexity Analysis
