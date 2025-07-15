# 314. Binary Tree Vertical Order Traversal

## Question link
(https://leetcode.com/problems/binary-tree-vertical-order-traversal/)

## Question Description
Given a binary tree, return the vertical order traversal of its nodes' values. (ie, from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from left to right.

Example 1:
> Input: [3,9,20,null,null,15,7],
> 
> Output: [
>  [9],
>  [3,15],
>  [20],
>  [7]
> ]

Example 2:
> Input: [3,9,8,4,0,1,7],
>
> Output: [
>  [4],
>  [9],
>  [3,0,1],
>  [8],
>  [7]
> ]

Example 3:
> Input: [3,9,8,4,0,1,7,null,null,null,2,5] (0's right child is 2 and 1's left child is 5),
>
> Output: [
>  [4],
>  [9,5],
>  [3,0,1],
>  [8,2],
>  [7]
> ]

## Tags
- tree
- treemap

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
    //dfs 
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        map<int, vector<vector<int>>> colToNodes;
        dfs(root, 0, 0, colToNodes);
        vector<vector<int>> ans;
        
        for(auto it = colToNodes.begin(); it != colToNodes.end(); it++){
            vector<vector<int>> t = it->second;
            sort(t.begin(), t.end());
            vector<int> tt;
            for(int i = 0; i < t.size(); i++){
                tt.push_back(t[i][1]);
            }
            ans.push_back(tt);
        }

        return ans;
    }
    
    void dfs(TreeNode* root, int depth, int offset, map<int, vector<vector<int>>>& m){
        if(root == NULL) return;
        if(m.find(offset) == m.end()) m[offset] = {};
        m[offset].push_back({depth, root->val});
        dfs(root->left, depth + 1, offset -1, m);
        dfs(root->right, depth + 1, offset + 1, m);
    }
};
```

## Time Complexity Analysis
Running time  : O(n)