# 450. Delete Node in a BST

## Question link
(https://leetcode.com/problems/delete-node-in-a-bst/)

## Question Description
Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.
Basically, the deletion can be divided into two stages:
1. Search for a node to remove.
2. If the node is found, delete the node.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/09/04/del_node_1.jpg" width="400" />
>
> Input: root = [5,3,6,2,4,null,7], key = 3
>
> Output: [5,4,6,2,null,null,7]
>
> Explanation: Given key to delete is 3. So we find the node with value 3 and delete it.
> One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
> Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.
>
> <img src="https://assets.leetcode.com/uploads/2020/09/04/del_node_supp.jpg" width="200" />

Example 2:
> Input: root = [5,3,6,2,4,null,7], key = 0
>
> Output: [5,3,6,2,4,null,7]
>
> Explanation: The tree does not contain a node with value = 0.

Example 3:
> Input: root = [], key = 0
>
> Output: []

Constraints:
- The number of nodes in the tree is in the range [0, 10<sup>4</sup> ].
- -10<sup>5</sup>  <= Node.val <= 10<sup>5</sup> 
- Each node has a unique value.
- root is a valid binary search tree.
- -10<sup>5</sup>  <= key <= 10<sup>5</sup> 

Follow up: Could you solve it with time complexity O(height of tree)?
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
class Solution {
public:
    TreeNode* deleteNode(TreeNode* root, int key) {
        // find key
        if(root == NULL) return NULL;
        if(key < root->val){
            root->left = deleteNode(root->left, key);
        }else if(key > root->val){
            root->right = deleteNode(root->right, key);
        }else{
            // root->val == key, delete
            if(root->left  == NULL) return root->right;
            if(root->right == NULL) return root->left;

            root->val = _findMin(root->right);
            root->right = deleteNode(root->right, root->val);
        }

        return root;
    }

    int _findMin(TreeNode* node){
        while(node->left != NULL) node = node->left;
        return node->val;
    }
};
```

## Time Complexity Analysis
Running time  : O(log(n))
running space : O(h)