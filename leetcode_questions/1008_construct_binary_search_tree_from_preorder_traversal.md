# 1008. Construct Binary Search Tree from Preorder Traversal

## Question link
(https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/)

## Question Description
Given an array of integers preorder, which represents the preorder traversal of a BST (i.e., binary search tree), construct the tree and return its root.

It is guaranteed that there is always possible to find a binary search tree with the given requirements for the given test cases.

A binary search tree is a binary tree where for every node, any descendant of Node.left has a value strictly less than Node.val, and any descendant of Node.right has a value strictly greater than Node.val.

A preorder traversal of a binary tree displays the value of the node first, then traverses Node.left, then traverses Node.right.

Example 1:
>
> <img src="https://assets.leetcode.com/uploads/2019/03/06/1266.png" width="400" />
>
> Input: preorder = [8,5,1,7,10,12]
>
> Output: [8,5,10,1,7,null,12]

Example 2:
>
> Input: preorder = [1,3]
>
> Output: [1,null,3]

Constraints:
- 1 <= preorder.length <= 100
- 1 <= preorder[i] <= 1000
- All the values of preorder are unique.

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
    int idx;
public:
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        idx = 0;
        return _helper(preorder, INT_MIN, INT_MAX);
    }

    TreeNode* _helper(vector<int>& m, int lower, int upper){
        if(preorder.empty()) return NULL;
        if(idx >= m.size()) return NULL;
        int v = m[idx];
        if(v < lower || v > upper) {return NULL;}
        TreeNode* n = new TreeNode(v);
        idx++;
        n->left = _helper(m, lower, v);
        n->right = _helper(m, v, upper);
        return n;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)