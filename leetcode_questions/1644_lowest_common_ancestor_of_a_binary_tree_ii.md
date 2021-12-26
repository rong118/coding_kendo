# 1644. Lowest Common Ancestor of a Binary Tree II

## Question link
(https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-ii/)

## Question Description
Given the root of a binary tree, return the lowest common ancestor (LCA) of two given nodes, p and q. If either node p or q does not exist in the tree, return null. All values of the nodes in the tree are unique.
According to the definition of LCA on Wikipedia: "The lowest common ancestor of two nodes p and q in a binary tree T is the lowest node that has both p and q as descendants (where we allow a node to be a descendant of itself)". A descendant of a node x is a node y that is on the path from node x to some leaf node.

Example 1:
>
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
>
> Output: 3
>
> Explanation: The LCA of nodes 5 and 1 is 3.

Example 2:
>
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
>
> Output: 5
>
> Explanation: The LCA of nodes 5 and 4 is 5. A node can be a descendant of itself according to the definition of LCA.

Example 3:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 10
>
> Output: null
>
> Explanation: Node 10 does not exist in the tree, so return null.

Constraints:
- The number of nodes in the tree is in the range [1, 10<sup>4</sup>].
- -10<sup>9</sup> <= Node.val <= 10<sup>9</sup> 
- All Node.val are unique.
- p != q

Follow up: Can you find the LCA traversing the tree, without checking nodes existence?

<br/>

## 分类 && 解题思路
- tree
- bst

## Code Implementation
```c++
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if(_dfs(root, p) && _dfs(root, q)){
        return _lca(root, p, q);
    }else{
        return NULL;
    }
}

bool _dfs(TreeNode* root, TreeNode* target){
    if(root == NULL ) return false;
    if(root == target) return true;
    return _dfs(root->left, target) && _dfs(root->right, target);
     
}

TreeNode* _lca(TreeNode* root, TreeNode* p, TreeNode* q) {
    if(root == NULL || root == p || root == q) return root;
    TreeNode* l = _lca(root->left, p, q);
    TreeNode* r = _lca(root->right, p, q);
    if(l != NULL && r != NULL) return root;
    if(l == NULL && r != NULL) return r;
    if(l != NULL && r == NULL) return l;
    return NULL;
}
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)