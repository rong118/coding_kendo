# Word Search II

## Question link
(https://leetcode.com/problems/word-search-ii/)

## Question Description
Given an m x n board of characters and a list of strings words, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

> Example 1
>
>![Image](https://assets.leetcode.com/uploads/2020/11/07/search1.jpg)
>
> Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
>
> Output: ["eat","oath"]

> Example 2
>
>![Image](https://assets.leetcode.com/uploads/2020/11/07/search2.jpg)
>
> Input: board = [["a","b"],["c","d"]], words = ["abcb"]
>
> Output: []

Constraints:
- m == board.length
- n == board[i].length
- 1 <= m, n <= 12
- board[i][j] is a lowercase English letter.
- 1 <= words.length <= 3 * 10<sup>4</sup>
- 1 <= words[i].length <= 10
- words[i] consists of lowercase English letters.
- All the strings of words are unique.

## Tags
- dfs
- tire (用在空间优化)
- 从每一个位置暴力展开向4个方向，同时用Trie的searchPrefix来做减枝

## Code
```c++
class TrieNode {
public:
    vector<TrieNode*> children;
    bool isWord;
    TrieNode(){
        children.resize(26, NULL);
        isWord = false;
    }
};

class Trie {
private:
    TrieNode* root;

public:
    Trie(){
        root = new TrieNode();
    }

    void add(string word){
        TrieNode* node = root;
        for(char c : word){
            if(node->children[c - 'a'] == NULL){
                node->children[c - 'a'] = new TrieNode();
            }
            node = node->children[c - 'a'];
        }
        node->isWord = true;
    }

    bool search(string word){
        TrieNode* node = root;
        for(char c : word){
            if(node->children[c - 'a'] == NULL){
                return false;
            }
            node = node->children[c - 'a'];
        }

        return node->isWord;
    }

    bool searchPrefix(string word){
        TrieNode* node = root;
        for(char c : word){
            if(node->children[c - 'a'] == NULL){
                return false;
            }
            node = node->children[c - 'a'];
        }

        return true;
    }
};

class Solution {
private:
    std::unordered_set<string> s;
    std::vector<string> ans;
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        int M = board.size();
        int N = board[0].size();
        Trie* trie = new Trie();
        for(string word : words){
            trie->add(word);
        }
        vector<vector<bool> > visited(M, vector<bool>(N, false));

        string tmp;
        for(int i = 0; i < M; i++){
            for(int j = 0; j < N; j++){
                dfs(board, visited, tmp, i, j , trie);
            }
        }

        for (auto it = s.begin(); it != s.end(); it++) {
            ans.push_back(*it);
        }

        return ans;
    }

    void dfs(vector<vector<char>>& board, vector<vector<bool> > visited, string str, 
    int x, int y, Trie* trie){
        if(x < 0 || x >= board.size() || y < 0 || y >= board[0].size()) return;
        if(visited[x][y]) return;
        str += board[x][y];
        if(!trie->searchPrefix(str)) return; //减枝
        if(trie->search(str)) s.insert(str);
        visited[x][y] = true;
        vector<vector<int> > dirs = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        for(int i = 0; i < dirs.size(); i ++){
            dfs(board, visited, str, x + dirs[i][0], y + dirs[i][1], trie);
        }
        visited[x][y] = false;
        return;
    }
};
```

## Time Complexity Analysis
- O(M * N)