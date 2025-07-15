# 449. Serialize and Deserialize BST

## Question link
(https://leetcode.com/problems/serialize-and-deserialize-bst/)

## Question Description
Serialization is converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary search tree. There is no restriction on how your serialization/deserialization algorithm should work. You need to ensure that a binary search tree can be serialized to a string, and this string can be deserialized to the original tree structure.

The encoded string should be as compact as possible.

Example 1:
>
> Input: root = [2,1,3]
>
> Output: [2,1,3]

Example 2:
>
> Input: root = []
>
> Output: []

Constraints:
- The number of nodes in the tree is in the range [0, 10<sup>4</sup> ].
- 0 <= Node.val <= 10<sup>4</sup>
- The input tree is guaranteed to be a binary search tree.

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
    // Per BST, we don't need to store empty node into string but comparing value to decide node end during deserialize
    string serialize(TreeNode* root) {
        if(root == NULL) return "";
        string res = to_string(root->val);
        if(root->left != NULL) res += "/" + serialize(root->left);
        if(root->right != NULL) res += "/" + serialize(root->right);
        return res;
    }

    // Decodes your encoded data to tree.
    // Use <lower upper>
    TreeNode* deserialize(string data) {
        if(data == "") return NULL;
        //cout<< data <<endl;
        idx = 0; // reset idx
        vector<string> m;
        
        _split(data, m, '/');
        return _helper(m, INT_MIN, INT_MAX);
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

    TreeNode* _helper(vector<string>& m, int lower, int upper){
        if(idx >= m.size()) { return NULL;}
        string s = m[idx];
        // cout << "# " << s << endl;
        if(stoi(s) < lower || stoi(s) > upper) { return NULL; }
        TreeNode* root = new TreeNode(stoi(s));
        idx++;
        root->left  = _helper(m, lower, stoi(s));
        root->right = _helper(m, stoi(s), upper);

        return root;
    }
};


// Your Codec object will be instantiated and called as such:
// Codec* ser = new Codec();
// Codec* deser = new Codec();
// string tree = ser->serialize(root);
// TreeNode* ans = deser->deserialize(tree);
// return ans;
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)