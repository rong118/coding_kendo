# 1372. Longest ZigZag Path in a Binary Tree

## Question link
(https://leetcode.com/problems/longest-zigzag-path-in-a-binary-tree/)

## Question Description
You are given the root of a binary tree.

A ZigZag path for a binary tree is defined as follow:

- Choose any node in the binary tree and a direction (right or left).
- If the current direction is right, move to the right child of the current node; otherwise, move to the left child.
- Change the direction from right to left or from left to right.
- Repeat the second and third steps until you can't move in the tree.

Zigzag length is defined as the number of nodes visited - 1. (A single node has a length of 0).

Return the longest ZigZag path contained in that tree.

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/01/22/sample_1_1702.png" width="200" />
>
> Input: root = [1,null,1,1,1,null,null,1,1,null,1,null,null,null,1,null,1]
>
> Output: 3
>
> Explanation: Longest ZigZag path in blue nodes (right -> left -> right).

Example 2:
> <img src="https://assets.leetcode.com/uploads/2020/01/22/sample_2_1702.png" width="200" />
>
> Input: root = [1,1,1,null,1,null,null,1,1,null,1]
>
> Output: 4
>
> Explanation: Longest ZigZag path in blue nodes (left -> right -> left -> right).

Constraints:
- The number of nodes in the tree is in the range [1, 5 * 10<sup>4</sup>].
- 1 <= Node.val <= 100

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
    int res = 0;
public:
    int longestZigZag(TreeNode* root) {
        _dfs(root, true);
        _dfs(root, false);
        return res;
    }
    
    int _dfs(TreeNode* node, bool isLeft){
        if(root == NULL) return 0;
        int left = dfs(root->left, true);
        int right = dfs(root->right, false);
        res = max(res, max(left, right));
        return isLeft ? 1 + right : 1 + left;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)