# 145. Binary Tree Postorder Traversal

## Question link
(https://leetcode.com/problems/binary-tree-postorder-traversal/)

## Question Description
Given the root of a binary tree, return the postorder traversal of its nodes' values.

Example 1:
Input: root = [1,null,2,3]
Output: [3,2,1]

Example 2:
Input: root = []
Output: []

Example 3:
Input: root = [1]
Output: [1]

Example 4:
Input: root = [1,2]
Output: [2,1]

Example 5:
Input: root = [1,null,2]
Output: [2,1]


![Image]()
<img src="" width="400" />

Example
> example's description

Constraints:
- The number of the nodes in the tree is in the range [0, 100].
- -100 <= Node.val <= 100

## Tags


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
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        helper(root, res);
        return res;
    }
    
    // recursive
    void helper(TreeNode* root, vector<int>& ans){
        if(root == NULL) return;
        helper(root->left, ans);
        helper(root->right, ans);
        ans.push_back(root->val);
    }

    // iterative
    void helper(TreeNode* root, vector<int>& ans){
        if(root == NULL) return;
        stack<TreeNode*> stk;
        stk.push(root);
        while(!stk.empty()){
            root = stk.top();
            stk.pop();
            ans.insert(ans.begin(), root->val);
            if(root->left != NULL)
                stk.push(root->left);
            if(root->right != NULL)
                stk.push(root->right);
        }
    }
};
```

## Time Complexity Analysis
Running time  : O(n)