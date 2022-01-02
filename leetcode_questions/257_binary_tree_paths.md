# 257. Binary Tree Paths

## Question link
(https://leetcode.com/problems/binary-tree-paths/)

## Question Description
Given the root of a binary tree, return all root-to-leaf paths in any order.

A leaf is a node with no children.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/03/12/paths-tree.jpg" width="400" />
>
> Input: root = [1,2,3,null,5]
>
> Output: ["1->2->5","1->3"]

Example 2:
>
> Input: root = [1]
>
> Output: ["1"]

<br/>

Constraints:
- The number of nodes in the tree is in the range [1, 100].
- -100 <= Node.val <= 100

## 分类 && 解题思路
- tree
- dfs

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
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> ans;
        string path = "";
        _helper(root, path, ans);
        return ans;
    }

    void _helper(TreeNode* root, string path, vector<string>& ans){
        if(root == NULL) return;
        
        if(path != "") {
            path += "->";
        }
        path += to_string(root->val);
        
        if(root->left == NULL && root->right == NULL) {
            ans.push_back(path);
            return;
        }
        
        _helper(root->left, path, ans);
        _helper(root->right, path, ans);
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)