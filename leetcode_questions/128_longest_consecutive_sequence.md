# 128 Longest Consecutive Sequence

## Question link
(https://leetcode.com/problems/longest-consecutive-sequence/)

## Question Description
Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

Example 1:
> Input: nums = [100,4,200,1,3,2]
>
> Output: 4
>
> Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

Example 2:
> Input: nums = [0,3,7,2,5,8,4,6,0,1]
>
> Output: 9

Constraints:
- 0 <= nums.length <= 10<sup>5</sup>
- -10<sup>9</sup> <= nums[i] <= 10<sup>9</sup>

## 分类 && 解题思路
- hashset
- unionfind

## Code Implementation
```c++
// solution 1 hashset
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        set<int> s(nums.begin(), nums.end());
        int res = 0;
        for(int i=0;i<nums.size();i++){
            
            if(s.find(nums[i]-1)==s.end()){
                int x = nums[i];
                
                int count = 0;
                while(s.find(x)!=s.end()){
                    
                    count++;
                    x++;
                }
                
                res = max(res, count);
            }
        }
        
        return res;
    }
};

// solution 2 union find
class DSU {
public:
    vector<int> parent;
    vector<int> size;
    DSU(int N){
        parent.resize(N);
        size.resize(N, 1);
        for(int i = 0; i < N; i++) parent[i] = i;
    }

    int _find(int x){
        if(parent[x] != x) parent[x] = _find(parent[x]);
        return parent[x];
    }

    void _union(int x, int y){
        int rootX = _find(x);
        int rootY = _find(y);
        if(rootX == rootY) return;
        if(size[rootX] <= size[rootY]){
            parent[rootX] = rootY;
            size[rootY] += size[rootX];
        }else{
            parent[rootY] = rootX;
            size[rootX] += size[rootY];
        }
    }

    int _findmax(){
        int ans = 0;
        for(int s : size) ans = max(ans, s);
        return ans;
    }
};

class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        DSU* dsu = new DSU(nums.size());
        unordered_map<int, int> m;
        for(int i = 0; i < nums.size(); i++){
            if(m.find(nums[i]) != m.end()) continue;
            m[nums[i]] = i;
            if(m.find(nums[i] + 1) != m.end()) dsu->_union(i, m[nums[i] + 1]);
            if(m.find(nums[i] - 1) != m.end()) dsu->_union(i, m[nums[i] - 1]);
        }

        return dsu->_findmax();
    }
};
```

## Time Complexity Analysis
Running time  : O(n)