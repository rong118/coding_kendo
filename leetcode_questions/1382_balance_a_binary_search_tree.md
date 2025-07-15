# 1382. Balance a Binary Search Tree

## Question link
(https://leetcode.com/problems/balance-a-binary-search-tree/)

## Question Description
Given the root of a binary search tree, return a balanced binary search tree with the same node values. If there is more than one answer, return any of them.

A binary search tree is balanced if the depth of the two subtrees of every node never differs by more than 1

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/08/10/balance1-tree.jpg" width="400" />
>
> Input: root = [1,null,2,null,3,null,4,null,null]
>
> Output: [2,1,3,null,null,null,4]
>
> Explanation: This is not the only correct answer, [3,1,4,null,2] is also correct.

Example 2:
> <img src="https://assets.leetcode.com/uploads/2021/08/10/balanced2-tree.jpg" width="400" />
>
> Input: root = [2,1,3]
>
> Output: [2,1,3]

Constraints:
- The number of nodes in the tree is in the range [1, 10<sup>4</sup>].
- 1 <= Node.val <= 10<sup>5</sup> 

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
public:
    TreeNode* balanceBST(TreeNode* root) {
        vector<int> arr;
        _inorder(root, arr);
        return _generate_blanace_bst(arr, 0, arr.size()-1);
    }
    
    void _inorder(TreeNode* root, vector<int>& arr){
        if(root == NULL) return;
        _inorder(root->left, arr);
        arr.push_back(root->val);
        _inorder(root->right, arr);
        return;
    }
    
    TreeNode* _generate_blanace_bst(vector<int>& arr, int left, int right){
        if(left > right) return NULL;
        int mid = (left + right)/2;
        TreeNode* root = new TreeNode(arr[mid]);
        root->left = _generate_blanace_bst(arr, left, mid-1);
        root->right = _generate_blanace_bst(arr, mid + 1, right);
        
        return root;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)