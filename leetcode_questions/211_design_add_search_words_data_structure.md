# 211. Design Add and Search Words Data Structure

## Question link
(https://leetcode.com/problems/design-add-and-search-words-data-structure/)

## Question Description
Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:
- WordDictionary() Initializes the object.
- void addWord(word) Adds word to the data structure, it can be matched later.
- bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

Example
> Input:
>
> ["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
> [[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
>
> Output:
>
> [null,null,null,null,false,true,true,true]
>
> Explanation:
> WordDictionary wordDictionary = new WordDictionary();
> wordDictionary.addWord("bad");
> wordDictionary.addWord("dad");
> wordDictionary.addWord("mad");
> wordDictionary.search("pad"); // return False
> wordDictionary.search("bad"); // return True
> wordDictionary.search(".ad"); // return True
> wordDictionary.search("b.."); // return True

Constraints:
- 1 <= word.length <= 500
- word in addWord consists lower-case English letters.
- word in search consist of  '.' or lower-case English letters.
- At most 50000 calls will be made to addWord and search.

## Tags
- Trie
- DFS
- backtracking

## Code
```c++
class TrieNode {
public:
    vector<TrieNode*> children;
    bool isWord;
    TrieNode(){
        //children may resize or update inital value
        children.resize(26, NULL);
        isWord = false;
    }
};

class WordDictionary {
private:
    TrieNode* root;

public:
    WordDictionary(){
        root = new TrieNode();
    }

    void addWord(string word){
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
        return helper(word, 0, root);
    }

    bool helper(string word, int pos, TrieNode* node){
        if(pos == word.size()) { return node->isWord; }
        char ch = word[pos];
        if(ch != '.'){
            return node->children[ch - 'a'] != NULL && 
                helper(word, pos + 1, node->children[ch - 'a']);
        }else{  // support match '.'
            for(int i = 0; i < 26; i++){
                if( node->children[i] != NULL && 
                helper(word, pos + 1, node->children[i])){
                    return true;
                }
            }
        }

        return false;
    }
};
```

## Time Complexity Analysis
Input word length is n.
Number of the nodes is v.
- insert()  => O(n)
- search()  => O(v)