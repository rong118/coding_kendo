# 865. Smallest Subtree with all the Deepest Nodes

## Question link
(https://leetcode.com/problems/smallest-subtree-with-all-the-deepest-nodes/)

## Question Description
Given the root of a binary tree, the depth of each node is the shortest distance to the root.

Return the smallest subtree such that it contains all the deepest nodes in the original tree.

A node is called the deepest if it has the largest depth possible among any node in the entire tree.

The subtree of a node is a tree consisting of that node, plus the set of all descendants of that node.

Example 1:
> <img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/01/sketch1.png" width="400" />
>
> Input: root = [3,5,1,6,2,0,8,null,null,7,4]
>
> Output: [2,7,4]
>
> Explanation: We return the node with value 2, colored in yellow in the diagram.
>
> The nodes coloured in blue are the deepest nodes of the tree.
>
> Notice that nodes 5, 3 and 2 contain the deepest nodes in the tree but node 2 is the smallest subtree among them, so we return it.

Example 2:
>
>
> Input: root = [1]
>
> Output: [1]
>
> Explanation: The root is the deepest node in the tree.

Example 3:
> Input: root = [0,1,3,null,2]
>
> Output: [2]
>
> Explanation: The deepest node in the tree is 2, the valid subtrees are the subtrees of nodes 2, 1 and 0 but the subtree of node 2 is the smallest.
 

Constraints:
- The number of nodes in the tree will be in the range [1, 500].
- 0 <= Node.val <= 500
- The values of the nodes in the tree are unique.

<br/>

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
 // same with lc1123
class Solution {
public:
    int _height(TreeNode* root){
        if(root == NULL) return 0;
        return 1 + max(_height(root->left), _height(root->right));
    }
    
    TreeNode* subtreeWithAllDeepest(TreeNode* root) {
        if(root == NULL) return NULL;
        int lh = _height(root->left);
        int rh = _height(root->right);
        if (lh == rh) return root;
        if(lh > rh){
            return subtreeWithAllDeepest(root->left);
        }else{
            return subtreeWithAllDeepest(root->right);
        }   
    }
};
```

## Time Complexity Analysis
