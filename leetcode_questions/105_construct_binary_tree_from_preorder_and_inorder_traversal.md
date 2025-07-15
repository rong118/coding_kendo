# 105. Construct Binary Tree from Preorder and Inorder Traversal

## Question link
(https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

## Question Description
Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/02/19/tree.jpg" width="300" />
>
> Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
>
> Output: [3,9,20,null,null,15,7]

Example 2:
> 
> Input: preorder = [-1], inorder = [-1]
>
> Output: [-1]

Constraints:
- 1 <= preorder.length <= 3000
- inorder.length == preorder.length
- -3000 <= preorder[i], inorder[i] <= 3000
- preorder and inorder consist of unique values.
- Each value of inorder also appears in preorder.
- preorder is guaranteed to be the preorder traversal of the tree.
- inorder is guaranteed to be the inorder traversal of the tree.

## Tags
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
    int preorderIdx = 0;
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        preorderIdx = 0;
        unordered_map<int, int> m;
        for(int i = 0; i < inorder.size(); i++) {
            m[inorder[i]] = i;
        }

        return _helper(0, inorder.size() - 1, preorder, inorder, m);
    }

    TreeNode* _helper(int start, int end, vector<int>& preorder, vector<int>& inorder, unordered_map<int, int>& m){
        if(start > end) return NULL;
        int v = preorder[preorderIdx++];
        int idx = m[v];
        TreeNode* root = new TreeNode(v);
        root->left  = _helper(start, idx - 1, preorder, inorder, m);
        root->right = _helper(idx + 1, end, preorder, inorder, m);
        return root;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)