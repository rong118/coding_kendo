# 236. Lowest Common Ancestor of a Binary Tree

## Question link
(https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

## Question Description

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”


![Image]()
<img src="https://assets.leetcode.com/uploads/2018/12/14/binarytree.png" width="400" />

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2018/12/14/binarytree.png" width="400" />
>
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
> Output: 3
> Explanation: The LCA of nodes 5 and 1 is 3.

Example 2:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
>
> Output: 5
>
> Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.

Example 3:
> Input: root = [1,2], p = 1, q = 2
>
> Output: 1

Constraints:
- The number of nodes in the tree is in the range [2, 10<sup>5</sup>].
- -10<sup>9</sup> <= Node.val <= 10<sup>9</sup> 
- All Node.val are unique.
- p != q
- p and q will exist in the tree.

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
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    // recusive
    // check left and right subtree and return LCA
    // divide and conquer
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == NULL || root == p || root == q) return root;
        TreeNode* l = lowestCommonAncestor(root->left, p, q);
        TreeNode* r = lowestCommonAncestor(root->right, p, q);
        if(l != NULL && r != NULL) return root;
        if(l == NULL && r != NULL) return r;
        if(l != NULL && r == NULL) return l;
        return NULL;
    }

    // iterative by build a parent map
    unordered_map<TreeNode*, TreeNode*> parent;
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        _dfs(null, root);
        set<TreeNode*> ancestors;
        while(p != NULL){
            ancestors.push(p);
            p = parent[p];
        }
        while(ancestors.find(q) == ancestors.end()){
            q = parent[q]
        }
        return q;
    } 

    _dfs(TreeNode* parentNode, TreeNode* cur){
        if(cur == nullptr) return;
        parent.put(cur, parentNode);
        dfs(cur, cur->left);
        dfs(cur, cur->right);
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)