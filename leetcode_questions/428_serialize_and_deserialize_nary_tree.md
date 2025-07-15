# 428. Serialize and Deserialize N-ary Tree

## Question link
(https://leetcode.com/problems/serialize-and-deserialize-n-ary-tree/)

## Question Description
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize an N-ary tree. An N-ary tree is a rooted tree in which each node has no more than N children. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that an N-ary tree can be serialized to a string and this string can be deserialized to the original tree structure.


For example, you may serialize the following 3-ary tree:

as [1 [3[5 6] 2 4]]. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

Note:
N is in the range of [1, 1000].
Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

List
- N is in the range of [1, 1000].
- Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

## Tags
- tree

## Code Implementation
```c++
class Codec {
    int idx = 0;
public:
    string serialize(Node* root){
        idx = 0;
        string s;
        dfs(root, s);
        return s;
    }

    void dfs(Node* root, string& l){
        if(root == NULL) return;
        l += to_string(root->val);
        l += " ";
        l += to_string(root->children.size());
        l += " ";
        for(int i = 0; i < root->children; i++){
            dfs(root->children[i], l);
        }
    }

    Node* deserialize(string data) {
        vector<string> m;
        
        _split_space(data, m);
        return _helper(m);
    }

    //
    void _split_space(string& s, vector<string>& m){
        stringstream ss(s);
        string word;
        while (ss >> word) {
            m.push_back(m)
        }
    }

    TreeNode* _helper(vector<string>& m){
        string v = m[idx++];
        string children_num = m[idx++];
        TreeNode* root = NULL;
        root = new TreeNode(stoi(v));
        for(int i = 0; i < stoi(children_num); i++){
            root->children.push_back(_helper(m));
        }

        return root;
    }
}
```

## Time Complexity Analysis
Running time  : O(n)
running space : O(n)