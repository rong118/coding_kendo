# 549 Binary Tree Longest Consecutive Sequence II

## Question link
(https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii/)

## Question Description
Given a binary tree, you need to find the length of Longest Consecutive Path in Binary Tree.

Especially, this path can be either increasing or decreasing. For example, [1,2,3,4] and [4,3,2,1] are both considered valid, but the path [1,2,4,3] is not valid. On the other hand, the path can be in the child-Parent-child order, where not necessarily be parent-child order.

Example 1:
>
> Input:
>
>        1
>       / \
>      2   3
>
> Output: 2
>
> Explanation: The longest consecutive path is [1, 2] or [2, 1].

Example 2:
> Input:
>
>        2
>       / \
>      1   3
>
> Output: 3
>
> Explanation: The longest consecutive path is [1, 2, 3] or [3, 2, 1].

<br/>

Note: All the values of tree nodes are in the range of [-1e7, 1e7].

## Tags
- tree
- dfs

## Code Implementation
```c++
class Solution {
    int maxval = 0;
    int longestConsecutive(TreeNode* root){
        _longestPath(root);
        return maxval;
    }

    vector<int> _longestPath(TreeNode* root){
        if(root == NULL) return {0, 0};
        int inc = 1, dcr = 1;
        if(root->left != NULL){
            vector<int> l = _longestPath(root->left);
            if(root->val == root->left->val + 1){
                dcr = l[1] + 1;
            }else if(root->val == root->left->val - 1){
                inc = l[0] + 1;
            }
        }

        if(root->right != NULL){
            vector<int> r = _longestPath(root->left);
            if(root->val == root->right->val + 1){
                dcr = max(dcr, r[1] + 1);
            }else if(root->val == root->right->val - 1){
                inc = max(inc, r[0] + 1);
            }

        }
        maxval = max(maxval, dcr + inc - 1);
        return {inc, dcr};
    }
}
```

## Time Complexity Analysis
