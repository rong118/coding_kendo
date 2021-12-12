# 102. Binary Tree Level Order Traversal

## Question link
(https://leetcode.com/problems/binary-tree-level-order-traversal/)

## Question Description
Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg" width="300" />
> 
> Input: root = [3,9,20,null,null,15,7]
>
> Output: [[3],[9,20],[15,7]]

Example 2:
> Input: root = [1]
>
> Output: [[1]]

Example 3:
> Input: root = []
>
> Output: []

Constraints:
- The number of nodes in the tree is in the range [0, 2000].
- -1000 <= Node.val <= 1000

## 分类 && 解题思路
- tree
- bfs

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
    //bfs
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int> > ans;
        vector<int> tmp;
        queue<TreeNode*> que;
        TreeNode* flagNode=new TreeNode(INT_MAX); 
        if(root == NULL) return ans;
        que.push(root);
        que.push(flagNode);
        while(1){
            root = que.front(); que.pop();
            if(root->val == INT_MAX){
                ans.push_back(tmp);
                if(que.empty()) break;
                que.push(flagNode);
                tmp.clear();
            }else{
                tmp.push_back(root->val);
                if(root->left != NULL)
                    que.push(root->left);
                if(root->right != NULL)
                    que.push(root->right);
            }
        }

        return ans;
    }

    // dfs & recursive
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ret;
        dfs(root, ret, 0);
        return ret;
    }

    void dfs(TreeNode* root, vector<vector<int>>& ret, int height){
        if(root == NULL) return;
        if(height == ret.size()) ret.push_back({});
        ret[height].push_back(root->val);
        if(root->left != NULL)
            dfs(root->left, ret, height + 1);
        if(root->right != NULL)
            dfs(root->right, ret, height + 1);
    }
};
```

## Time Complexity Analysis
Running time : O(n)