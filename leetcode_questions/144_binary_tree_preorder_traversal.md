# 144. Binary Tree Preorder Traversal

## Question link
(https://leetcode.com/problems/binary-tree-preorder-traversal/)

## Question Description
Given the root of a binary tree, return the preorder traversal of its nodes' values.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg" width="400" /> 
> Input: root = [1,null,2,3]
>
> Output: [1,2,3]

Example 2:
> Input: root = []
>
> Output: []

Example 3:
> Input: root = [1]
>
> Output: [1]

Example 4:
> Input: root = [1,2]
>
> Output: [1,2]

Example 5:
> Input: root = [1,null,2]
>
> Output: [1,2]

Constraints:
- The number of nodes in the tree is in the range [0, 100].
- -100 <= Node.val <= 100

## 分类 && 解题思路
- tree

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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        helper(root, res);
        return res;
    }

    // recursive
    void helper(TreeNode* root, vector<int>& ans){
        if(root == NULL) return;
        ans.push_back(root->val);
        helper(root->left, ans);
        helper(root->right, ans);
    }

    // iterative
    void helper(TreeNode* root, vector<int>& ans){
        if(root == NULL) return;
        stack<TreeNode*> stk;
        stk.push(root);
        while(!stk.empty()){
            root = stk.top();
            stk.pop();
            ans.push_back(root->val);
            if(root->right != NULL) 
                stk.push(root->right);
            if(root->left != NULL)
                stk.push(root->left);
        }
    }
};
```

## Time Complexity Analysis
Running time  : O(n)