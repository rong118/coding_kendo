# 889. Construct Binary Tree from Preorder and Postorder Traversal

## Question link
(https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)

## Question Description
Given two integer arrays, preorder and postorder where preorder is the preorder traversal of a binary tree of distinct values and postorder is the postorder traversal of the same tree, reconstruct and return the binary tree.

If there exist multiple answers, you can return any of them.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/07/24/lc-prepost.jpg" width="300" />
>
> Input: preorder = [1,2,4,5,3,6,7], postorder = [4,5,2,6,7,3,1]
>
> Output: [1,2,3,4,5,6,7]

Example 2:
>
> Input: preorder = [1], postorder = [1]
>
> Output: [1]

Constraints:
- 1 <= preorder.length <= 30
- 1 <= preorder[i] <= preorder.length
- All the values of preorder are unique.
- postorder.length == preorder.length
- 1 <= postorder[i] <= postorder.length
- All the values of postorder are unique.
- It is guaranteed that preorder and postorder are the preorder traversal and postorder traversal of the same binary tree.

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
    TreeNode* constructFromPrePost(vector<int>& preorder, vector<int>& postorder) {
        unordered_map<int, int> m;
        for(int i = 0; i < postorder.size(); i++){
            m[postorder[i]] = i;
        }

        return _helper(0, preorder.size() - 1, 0, postorder.size() - 1, preorder, postorder, m);
    }

    TreeNode* _helper(int preLeft, int preRight, int postLeft, int postRight, vector<int>& preorder, vector<int>& postorder, unordered_map<int, int>& m){
        if(preLeft > preRight || postLeft > postRight) {return NULL;}
        if(preLeft == preRight) return new TreeNode(preorder[preLeft]); // otherwise cannot 
        TreeNode* root = new TreeNode(preorder[preLeft]);
        int index = m[preorder[preLeft + 1]];
        int leftTreeSize = index - postLeft + 1;
        root->left  = _helper(preLeft + 1, preLeft + leftTreeSize, postLeft, postLeft + leftTreeSize - 1, preorder, postorder, m);
        root->right = _helper(preLeft + leftTreeSize + 1, preRight, postLeft + leftTreeSize, postRight - 1, preorder, postorder, m);
        return root;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)