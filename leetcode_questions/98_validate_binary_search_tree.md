# 98. Validate Binary Search Tree

## Question link
(https://leetcode.com/problems/validate-binary-search-tree/)

## Question Description
Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:
- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg" width="400" />
>
> Input: root = [2,1,3]
>
> Output: true

Example 2:
> <img src="https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg" width="400" />
> 
> Input: root = [5,1,4,null,null,3,6]
>
> Output: false
>
> Explanation: The root node's value is 5 but its right child's value is 4.

Constraints:
- The number of nodes in the tree is in the range [1, 10<sup>4</sup>].
- -2<sup>31</sup> <= Node.val <= 2<sup>31</sup> - 1

## Tags
- tree
- bst

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

// recursive
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return _valid(root, LONG_MIN, LONG_MAX);
    }
    
    bool _valid(TreeNode* root, long minVal, long maxVal) {
        if (root == NULL) return true;
        if (root->val >= maxVal || root->val <= minVal) return false;
        return _valid(root->left, minVal, root->val) && _valid(root->right, root->val, maxVal);
    }
};

// iterative
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        TreeNode* pre = NULL;
        stack<TreeNode*> stk;
        while(root != NULL || !stk.empty()){
            while(root != NULL){
                stk.push(root);
                root = root->left;
            }
            root = stk.pop();
            if(pre != NULL && root->val <= pre->val){ return false;}
            pre = root;
            root = root->right;
        }
        return true;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(1)