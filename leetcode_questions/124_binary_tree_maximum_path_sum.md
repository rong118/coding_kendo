# 124. Binary Tree Maximum Path Sum

## Question link
(https://leetcode.com/problems/binary-tree-maximum-path-sum/)

## Question Description
A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the root of a binary tree, return the maximum path sum of any non-empty path.


Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg" width="400" />
>
> Input: root = [1,2,3]
>
> Output: 6
>
> Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.

Example 2:
> <img src="https://assets.leetcode.com/uploads/2020/10/13/exx2.jpg" width="400" />
>
> Input: root = [-10,9,20,null,null,15,7]
>
> Output: 42
>
> Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.

<br/>

Example
> example's description

Constraints:
- The number of nodes in the tree is in the range [1, 3 * 10<sup>4</sup>].
- -1000 <= Node.val <= 1000

## Tags
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
    int maxV = INT_MIN;
public:
    int maxPathSum(TreeNode* root) {
        _dfs(root);
        return maxV;
    }

    int _dfs(TreeNode* root){
        if(root == NULL){
            return 0;
        }

        int left = max(0, _dfs(root->left));
        int right = max(0, _dfs(root->right));
        maxV = max(maxV, (left + right + root->val));
        return max(left, right) + root->val;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(1)