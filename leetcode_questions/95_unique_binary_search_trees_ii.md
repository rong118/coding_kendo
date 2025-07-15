# 95. Unique Binary Search Trees II

## Question link
(https://leetcode.com/problems/unique-binary-search-trees-ii/)

## Question Description
Given an integer n, return all the structurally unique BST's (binary search trees), which has exactly n nodes of unique values from 1 to n. Return the answer in any order.

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg" width="400" />
>
> Input: n = 3
> 
> Output: [[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]

Example 2:
> Input: n = 1
>
> Output: [[1]]

Constraints:
- 1 <= n <= 8

## Tags
- tree
- dfs

## Code Implementation
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<TreeNode*> generateTrees(int n) {
        vector<TreeNode*> m = _helper(1, n);
        return m;
    }
    
    vector<TreeNode*> _helper(int start, int end){
        vector<TreeNode*> m;
        if(start > end) return {NULL};
        if(start == end) {
            TreeNode* root = new TreeNode(start);
            return {root};
        }
        
        for(int i = start; i <= end; i++){
            vector<TreeNode*> l = _helper(start, i - 1);
            vector<TreeNode*> r = _helper(i + 1, end);
            for(int j = 0; j < l.size(); j++){
                for(int k = 0; k < r.size(); k++){
                    TreeNode* root = new TreeNode(i);
                    root->left = l[j];
                    root->right = r[k];
                    m.push_back(root);
                }
            }
        }
        
        return m;
    }
};
```

## Time Complexity Analysis
Difficult part : check catalan number 

Running time  : O(~ c^n)
running space : O(~ n*Tree())