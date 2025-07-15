# 421. Maximum XOR of Two Numbers in an Array

## Question link
(https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/)

## Question Description
Given an integer array nums, return the maximum result of nums[i] XOR nums[j], where 0 <= i <= j < n.

> Example 1:
>
> Input: nums = [3,10,5,25,2,8]
>
> Output: 28
>
> Explanation: The maximum result is 5 XOR 25 = 28.

> Example 2:
>
> Input: nums = [0]
>
> Output: 0

> Example 3:
>
> Input: nums = [2,4]
>
> Output: 6

> Example 4:
>
> Input: nums = [8,10,2]
>
> Output: 10

> Example 5:
>
> Input: nums = [14,70,53,83,49,91,36,80,92,51,66,70]
>
> Output: 127

Constraints:
- 1 <= nums.length <= 2 * 10<sup>5</sup>
- 0 <= nums[i] <= 2<sup>31</sup> - 1

## Tags
- trie
- bitwise
- bitwise trie 存入数字后，再次遍历从最高位找相反的bit，则可以形成最大的XOR,因为XOR只有不同才能留下

## C++ Implementation
```c++
class TrieNode {
public:
    vector<TrieNode*> children;
    TrieNode(){
        children.resize(2, NULL);
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
    }

    int findMaxXor(TrieNode* root, int num){
        int sum = 0;
        TrieNode* cur = root;
        string ss;
        for(int i = 31; i >= 0; i--){
            int curBit = (num >> i) & 1;
            int otherChoice = curBit == 1 ? 0 : 1;
            if(cur->children[otherChoice] == NULL){
                cur = cur->children[curBit];
            }else{
                sum += (1 << i);
                cur = cur->children[otherChoice];
            }
        }

        return sum;
    }
};

class Solution {
public:
    int findMaximumXOR(vector<int>& nums) {
        int res = INT_MIN;
        TrieNode * root = new TrieNode();
        for(int num : nums){
            root->addNum(root, num);
        }

        for(int num : nums){            
            res = max(root->findMaxXor(root, num), res);
        }

        return res;
    }
};
```

## Time Complexity Analysis
- O(n)