# 103. Binary Tree Zigzag Level Order Traversal

## Question link
> link

## Question Description
Given the root of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg" width="400" />
>
> Input: root = [3,9,20,null,null,15,7]
>
> Output: [[3],[20,9],[15,7]]

Example 2:
> Input: root = [1]
>
> Output: [[1]]

Example 3:
> Input: root = []
>
> Output: []
 
Constraints:
- The number of nodes in the tree is in the range [0, 2000].
- -100 <= Node.val <= 100

## Tags
- tree
- bfs

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
    // bfs
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int> > ans;
        vector<int> tmp;
        queue<TreeNode*> que;
        TreeNode* flagNode = new TreeNode(INT_MAX); 
        if(root == NULL) return ans;
        que.push(root);
        que.push(flagNode);
        while(1){
            root = que.front(); que.pop();
            if(root->val == INT_MAX){
                if(ans.size() % 2 == 1) {
                    reverse(tmp.begin(), tmp.end());
                }
                ans.push_back(tmp);
                if(que.empty()) break;
                que.push(flagNode);
                tmp.clear();
            }else{
                tmp.push_back(root->val);
                if(root->left != NULL)
                    que.push(root->left);
                if(root->right != NULL)
                    que.push(root->right);
            }
        }

        return ans;
    }

    // dfs & recursive
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int> > ans;
        dfs(root, ans, 0);
        return ans;
    }

    void dfs(TreeNode* root, vector<vector<int> >& ret, int height){
        if(root == NULL) return;
        if(height == ret.size()) ret.push_back({});
        if(height % 2 == 0) ret[height].push_back(root->val);
        if(height % 2 == 1) ret[height].insert(ret[height].begin(), root->val);
        if(root->left != NULL)
            dfs(root->left, ret, height + 1);
        if(root->right != NULL)
            dfs(root->right, ret, height + 1);
    }
};
```

## Time Complexity Analysis
Running time  : O(n)