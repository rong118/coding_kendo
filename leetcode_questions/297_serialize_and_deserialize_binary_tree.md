# 297. Serialize and Deserialize Binary Tree

## Question link
(https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

## Question Description
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

Example 1:
>
> <img src="https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg" width="400" />
>
> Input: root = [1,2,3,null,null,4,5]
>
> Output: [1,2,3,null,null,4,5]

Example 2:
>
> Input: root = []
>
> Output: []

Example 3:
>
> Input: root = [1]
>
> Output: [1]

Example 4:
>
> Input: root = [1,2]
>
> Output: [1,2]


Constraints:
- The number of nodes in the tree is in the range [0, 10n<sup>4</sup> ].
- -1000 <= Node.val <= 1000

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
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Codec {
public:
    int idx = 0;
    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        if(root == NULL) return "#";
        return to_string(root->val) + "/" + serialize(root->left) + "/" + serialize(root->right); 
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        // cout<< data <<endl;
        vector<string> m;
        
        _split(data, m, '/');
        return _helper(m);
    }

    // c++ pain point + 1 vs python/java
    void _split(const std::string& str,  vector<string>& cont, char delim = '/'){
        std::size_t current, previous = 0;
        current = str.find(delim);
        while (current != std::string::npos) {
            cont.push_back(str.substr(previous, current - previous));
            previous = current + 1;
            current = str.find(delim, previous);
        }
        cont.push_back(str.substr(previous, current - previous));
    }

    TreeNode* _helper(vector<string>& m){
        string s = m[idx++];
        TreeNode* root = NULL;
        if(s != "#") {
            root = new TreeNode(stoi(s));
            root->left  = _helper(m);
            root->right = _helper(m);
        }

        return root;
    }
};

// Your Codec object will be instantiated and called as such:
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));
```

## Time Complexity Analysis