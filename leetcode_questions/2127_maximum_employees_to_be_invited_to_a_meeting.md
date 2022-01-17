# 2127. Maximum Employees to Be Invited to a Meeting  ???? (TODO)

## Question link
(https://leetcode.com/problems/maximum-employees-to-be-invited-to-a-meeting/)

## Question Description
A company is organizing a meeting and has a list of n employees, waiting to be invited. They have arranged for a large circular table, capable of seating any number of employees.

The employees are numbered from 0 to n - 1. Each employee has a favorite person and they will attend the meeting only if they can sit next to their favorite person at the table. The favorite person of an employee is not themself.

Given a 0-indexed integer array favorite, where favorite[i] denotes the favorite person of the ith employee, return the maximum number of employees that can be invited to the meeting.

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/12/14/ex1.png" width="200" />
>
> Input: favorite = [2,2,1,2]
>
> Output: 3
>
> Explanation:
>
> The above figure shows how the company can invite employees 0, 1, and 2, and seat them at the round table.
>
> All employees cannot be invited because employee 2 cannot sit beside employees 0, 1, and 3, simultaneously.
>
> Note that the company can also invite employees 1, 2, and 3, and give them their desired seats.
>
> The maximum number of employees that can be invited to the meeting is 3.

Example 2:
> Input: favorite = [1,2,0]
>
> Output: 3
>
> Explanation: 
>
> Each employee is the favorite person of at least one other employee, and the only way the company can invite them is if they invite every employee.
>
> The seating arrangement will be the same as that in the figure given in example 1:
>
> - Employee 0 will sit between employees 2 and 1.
>
> - Employee 1 will sit between employees 0 and 2.
>
> - Employee 2 will sit between employees 1 and 0.
>
> The maximum number of employees that can be invited to the meeting is 3.

Example 3:
> <img src="https://assets.leetcode.com/uploads/2021/12/14/ex2.png" width="200" />
>
> Input: favorite = [3,0,1,4,1]
>
> Output: 4
>
> Explanation:
>
> The above figure shows how the company will invite employees 0, 1, 3, and 4, and seat them at the round table.
>
> Employee 2 cannot be invited because the two spots next to their favorite employee 1 are taken.
>
> So the company leaves them out of the meeting.
>
> The maximum number of employees that can be invited to the meeting is 4.

Constraints:
- n == favorite.length
- 2 <= n <= 10<sup>power</sup> 
- 0 <= favorite[i] <= n - 1
- favorite[i] != i

## 分类 && 解题思路
- graph
- topologic sort

## Code Implementation
```c++
// 有向图找环
class Solution {
    int N = 0;
    unordered_map<int, vector<int>> g;
    int singleMaxCyc = 0;
    vector<vector<int>> pairs;
    vector<int> f;
public:
    int maximumInvitations(vector<int>& favorite) {
        f = favorite;
        N = f.size();
        // build graph
        for(int i = 0; i < N; i++){
            int p =  f[i];
            if(g.find(p) == g.end()) {
                g[p] = {};
            }
            g[p].push_back(i);
        }

        // cycle count size
        _countCycle();
        return max(singleMaxCyc, _countSizeTwo());
    }

    void _countCycle(){
        vector<bool> visited(N, false);
        vector<bool> recStk(N, false);
        for(int i = 0; i < N; i++){
            _isCycUtil(i, recStk, visited, 0);
        }
    }

    void _isCycUtil(int i, vector<bool>& recStk, vector<bool>& visited, int count){
        if(recStk[i]){
            singleMaxCyc = max(singleMaxCyc, count);
            if(count == 2) pairs.push_back({i, f[i]});
            return;
        }

        if(visited[i]) return;
        visited[i] = true;
        recStk[i]  = true;
        vector<int> nei = g[i];
        for(int c : nei){
            _isCycUtil(c, recStk, visited, count + 1);
        }
        recStk[i]  = false;
    }

    unordered_map<int, int> m;
    int _countSizeTwo(){
        vector<bool> visited(N, false);
        int res = 0;
        for(vector<int> pair : pairs){
            int a = pair[0]; int b = pair[1];
            m[a] = 0;
            m[b] = 0;
            visited[a] = true;
            _dfs(b, visited, 0, b);
            visited[a] = false;

            visited[b] = true;
            _dfs(a, visited, 0, a);
            visited[b] = false;

            res += 2 + m[a] + m[b];
        }
        
        return res;
    }

    void _dfs(int cur, vector<bool>& visited, int len, int start){
        if(visited[cur]) return;
        m[start] = max(m[start], len);
        visited[cur] = true;
        for(int nei : g[cur]){
            if(!visited[nei]){
                _dfs(nei, visited, len + 1, start);
            }
        }
    }
};
```

## Time Complexity Analysis
