# 270 Closest Binary Search Tree Value

## Question link
(https://leetcode.com/problems/closest-binary-search-tree-value/)

## Question Description
Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

Note:
Given target value is a floating point.
You are guaranteed to have only one unique value in the BST that is closest to the target.

Example:
>
> Input: root = [4,2,5,1,3], target = 3.714286
>
>    4
>   / \
>  2   5
> / \
>1   3
> Output: 4

## 分类 && 解题思路
- tree
- bst

## Code Implementation
```c++
class Solution {
public:
    int closestValue(TreeNode* root, double target) {
        int res = root->val;
        while (root) {
            if (abs(res - target) >= abs(root->val - target)) {
                res = root->val;
            }
            root = target < root->val ? root->left : root->right;
        }

        return res;
    }
};
```

## Time Complexity Analysis
Running time  : O(h)
running space : O(1)