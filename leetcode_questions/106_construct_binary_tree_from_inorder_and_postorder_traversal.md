# 106. Construct Binary Tree from Inorder and Postorder Traversal

## Question link
(https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

## Question Description
Given two integer arrays inorder and postorder where inorder is the inorder traversal of a binary tree and postorder is the postorder traversal of the same tree, construct and return the binary tree.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/02/19/tree.jpg" width="300" />
>
> Input: inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
> 
> Output: [3,9,20,null,null,15,7]

Example 2:
> Input: inorder = [-1], postorder = [-1]
>
> Output: [-1]


Constraints:
- 1 <= inorder.length <= 3000
- postorder.length == inorder.length
- -3000 <= inorder[i], postorder[i] <= 3000
- inorder and postorder consist of unique values.
- Each value of postorder also appears in inorder.
- inorder is guaranteed to be the inorder traversal of the tree.
- postorder is guaranteed to be the postorder traversal of the tree.

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
    int postorderIdx = 0;
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        postorderIdx = postorder.size() - 1;
        unordered_map<int, int> m;
        for(int i = 0; i < inorder.size(); i++) {
            m[inorder[i]] = i;
        }

        return _helper(0, inorder.size() - 1, postorder, inorder, m);
    }

    TreeNode* _helper(int start, int end, vector<int>& postorder, vector<int>& inorder, unordered_map<int, int>& m){
        if(start > end) return NULL;
        int v = postorder[postorderIdx--];
        int idx = m[v];
        TreeNode* root = new TreeNode(v);
        root->right = _helper(idx + 1, end, postorder, inorder, m);
        root->left  = _helper(start, idx - 1, postorder, inorder, m);
        return root;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)