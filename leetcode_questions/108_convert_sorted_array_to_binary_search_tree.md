# 108. Convert Sorted Array to Binary Search Tree

## Question link
(https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

## Question Description
Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.

A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/02/18/btree1.jpg" width="400" />
>
> Input: nums = [-10,-3,0,5,9]
>
> Output: [0,-3,9,-10,null,5]
>
> Explanation: [0,-10,5,null,-3,null,9] is also accepted:

Example 2:
> <img src="https://assets.leetcode.com/uploads/2021/02/18/btree.jpg" width="400" />
>
> Input: nums = [1,3]
>
> Output: [3,1]
>
> Explanation: [1,3] and [3,1] are both a height-balanced BSTs.

Constraints:
- 1 <= nums.length <= 10<sup>4</sup> 
- -10<sup>4</sup>  <= nums[i] <= 10<sup>4</sup> 
- nums is sorted in a strictly increasing order.

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
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return _helper(nums, 0, nums.size() - 1);
    }

    TreeNode* _helper(vector<int>& nums, int start, int end){
        if(start > end) { return NULL;}
        int mid = (start + end)/2;
        
        TreeNode* root = new TreeNode(nums[mid]);
        root->left = _helper(nums, start, mid - 1);
        root->right = _helper(nums, mid + 1, end);
        return root;
    }
};
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)