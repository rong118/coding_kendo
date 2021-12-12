# 94. Binary Tree Inorder Traversal

## Question link
(https://leetcode.com/problems/binary-tree-inorder-traversal/)

## Question Description
Given the root of a binary tree, return the inorder traversal of its nodes' values.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg" width="400" />
> 
> Input: root = [1,null,2,3]
> 
> Output: [1,3,2]

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
> Output: [2,1]

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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        helper(root, res);
        return res;
    }

    // recursive
    void helper(TreeNode* root, vector<int>& ans){
        if(root == NULL) return;
        helper(root->left, ans);
        ans.push_back(root->val);
        helper(root->right, ans);
    }

    // iterative ++
    void helper(TreeNode* root, vector<int>& ans){
        stack<TreeNode*> stk;
        while(root != NULL || !stk.empty()){
            while(root != NULL){
                stk.push(root);
                root = root->left;
            }

            root = stk.top();
            stk.pop();
            ans.push_back(root->val);
            root = root->right;
        }
    }
};
```

## Time Complexity Analysis
Running time  : O(n)