# 1120 Maximum Average Subtree

## Question link
(https://leetcode.com/problems/maximum-average-subtree/)

## Question Description
Given the root of a binary tree, find the maximum average value of any subtree of that tree.

(A subtree of a tree is any node of that tree plus all its descendants. The average value of a tree is the sum of its values, divided by the number of nodes.) 

Example 1:
>
> Input: [5,6,1]
>
> Output: 6.00000
>
> Explanation: 
>
> For the node with value = 5 we have an average of (5 + 6 + 1) / 3 = 4.
>
> For the node with value = 6 we have an average of 6 / 1 = 6.
>
> For the node with value = 1 we have an average of 1 / 1 = 1.
>
> So the answer is 6 which is the maximum.

Note:
- The number of nodes in the tree is between 1 and 5000.
- Each node will have a value between 0 and 100000.
- Answers will be accepted as correct if they are within 10^-5 of the correct answer.

<br/>

## Tags
- tree

## Code Implementation
```c++
class Solution{
    double maxAvg = 0.0;
public:
    double maximumAverageSubtree(TreeNode* root){
        _dfs(root)
        return maxAvg;
    }

    pair<int, int> _dfs(TreeNode* root){
        if(root == NULL) return {0, 0};
        pair<int, int> left = _dfs(root->left);
        pair<int, int> right = _dfs(root->right);
        double r = (double)(left.first + right.first + root->val) / (double)(left.second + right.second + 1);
        maxAvg = max(maxAvg, r);
        return {left.first + right.first + root->val , left.second + right.second + 1};
    }
}
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(1)