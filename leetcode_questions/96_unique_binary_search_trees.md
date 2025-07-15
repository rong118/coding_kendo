# 96. Unique Binary Search Trees

## Question link
(https://leetcode.com/problems/unique-binary-search-trees/)

## Question Description
Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg" width="400" />
>
> Input: n = 3
>
> Output: 5

Example 2:
>
>
> Input: n = 1
>
> Output: 1

Constraints:
- 1 <= n <= 19

## Tags
- tree
- dp

## Code Implementation
```c++
class Solution {
public:
    int numTrees(int n) {
        vector<int> m(n + 1, 0);
        return _dfs(n, m);
    }

    int _dfs(int n, vector<int>& m){
        if(n == 0 || n == 1) return 1;
        if(m[n] != 0) return m[n];
        int sum = 0;
        for(int i = 1; i <= n; i++){
            sum += _dfs(i - 1, m) * _dfs(n - i, m);
        }
        m[n] = sum;
        return sum;
    }
};


// dp
// G(n) : the number of unique BST of array of length n.
// F(i, n) : the number of unique BST of array of length n and i as root.
// G(n) = sum(F(i, n)); (i from 1 to n);
// F(i, n) = G(i -1 ) * G(n - i)
// G(n) = sum(G(i -1 ) * G(n -i))
int numTrees(int n){
    vector<int> g(n + 1, 0);
    g[0] = 1;
    g[1] = 1;
    for(int i = 2; i <= n; i++){
        for(int j = 1; j <= i; j++){
            g[i] += g[j - 1] * g[i - j]
        }
    }

    return g[n]
}
```

## Time Complexity Analysis
Running time  : O(n^2)
running space : O(n)