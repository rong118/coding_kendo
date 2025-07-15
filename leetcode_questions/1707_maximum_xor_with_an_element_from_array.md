# 1707. Maximum XOR With an Element From Array

## Question link
(https://leetcode.com/problems/maximum-xor-with-an-element-from-array/)

## Question Description
You are given an array nums consisting of non-negative integers. You are also given a queries array, where queries[i] = [xi, mi].

The answer to the ith query is the maximum bitwise XOR value of xi and any element of nums that does not exceed mi. In other words, the answer is max(nums[j] XOR xi) for all j such that nums[j] <= mi. If all elements in nums are larger than mi, then the answer is -1.

Return an integer array answer where answer.length == queries.length and answer[i] is the answer to the ith query.

> Example 1:
>
> Input: nums = [0,1,2,3,4], queries = [[3,1],[1,3],[5,6]]
>
> Output: [3,3,7]
>
> Explanation:
> - 0 and 1 are the only two integers not greater than 1. 0 XOR 3 = 3 and 1 XOR 3 = 2. The larger of the two is 3.
> - 1 XOR 2 = 3.
> - 5 XOR 2 = 7.

> Example 2:
>
> Input: nums = [5,2,4,6,6,3], queries = [[12,4],[8,1],[6,3]]
>
> Output: [15,-1,5]

Constraints:
- 1 <= nums.length, queries.length <= 10<sup>5</sup>
- queries[i].length == 2
- 0 <= nums[j], xi, mi <= 10<sup>9</sup>

## Tags
- trie
- bitwise

## Code Implementation
```c++
bool comp(vector<int> &v1,vector<int> &v2)
{
    return v1[1]<v2[1];
}

class TrieNode {
public:
    vector<TrieNode*> children;
    int value;
    TrieNode(){
        children.resize(2, NULL);
        value = 0;
    }

    void addNum(TrieNode* root, int num){
        TrieNode* cur = root;
        for(int i = 31; i >= 0; i--){
            int curBit = (num >> i) & 1;
            if(cur->children[curBit] == NULL){
                cur->children[curBit] = new TrieNode();
            }
            cur = cur->children[curBit];
        }
        cur->value = num;
    }

    int findMaxXor(TrieNode* root, int num){
        TrieNode* cur = root;
        for(int i = 31; i >= 0; i--){
            int curBit = (num >> i) & 1;
            int otherChoice = curBit == 1 ? 0 : 1;
            if(cur->children[otherChoice] != NULL){
                cur = cur->children[otherChoice];
            }else if(cur->children[curBit] != NULL){
                cur = cur->children[curBit];
            }else{
                return -1;
            }
        }

        return num ^ cur->value;
    }
};

class Solution {
public:
    vector<int> maximizeXor(vector<int>& arr, vector<vector<int>>& queries) {
       vector<int> ans(queries.size());
        vector<vector<int>> query = queries;
        for(int i=0;i<query.size();i++)
        {
            // simply inserting query number so that we can put in order in ans as we are sorting the array
            query[i].push_back(i);
        }
        sort(arr.begin(),arr.end());
        sort(query.begin(),query.end(),comp);

        TrieNode * root = new TrieNode();
        int j = 0;

        for(int i = 0; i < query.size(); i++){
            vector<int> v = query[i];       
            int x = v[1];
            while(j<arr.size() && arr[j]<=x){
                root->addNum(root, arr[j]);
                j++;
            }
              
            ans[v[2]] = root->findMaxXor(root, v[0]);
        }

        return ans;
    }
};
```

## Time Complexity Analysis