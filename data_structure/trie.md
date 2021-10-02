# Trie
## 定义
Trie树，又叫字典树、前缀树(Prefix Tree)、 单词查找树 或 键树，是一种多叉树结构。N-array Tree

<img src="../assets/trie.png" width="300" />

## 特点
- 根节点(Root)不包含字符，除根节点外的每一个节点都仅 包含一个字符
- 从根节点到某一节点路径上所经过的字符连接起来，即为该节点对应的字符串;
- 任意节点的所有子节点所包含的字符都不相同;

## Use cases
- 自动补全
- spell check
- T9 打字预测

## methods
- addword()
- searchword()
- searchPrefix()

## Implementation 模版
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
```

## Bitwise Trie
每个node有2个分支，存的是0，1，Bitwise Trie represents a binary form of a number in nums, for example, 0 -> 0 -> 0 -> 1 -> 1 is 3
Bitwise Trie is a perfect way to see how different the binary forms of numbers are, for example, 3 and 2 share 4 bits

<img src="../assets/bitwise_trie.png" width="400" />

## Big O analysis
时间复杂度：
- 构建： 假设 n 个 字符， 每个长度k =>O(nk)
- 查找： 假设 字符 长度 k => O(k)

空间复杂度：
- 每个字典树 需要数组来维持 子节点， 所以内存消耗高

空间优化 ： 
- 使用hashmap 或者 红黑树 来代替 数组 保存子节点。 效率会变慢
- 缩点优化： 合并 只有一个子节点的节点

## Leetcode questions
- [208 Implement Trie](../leetcode_questions/208_implement_trie.md)
- [211 Design add and search words data structure](../leetcode_questions/211_design_add_search_words_data_structure.md)
- [212 Word Search II](../leetcode_questions/212_word_search_II.md)
- [421 Maximum XOR of Numbers in An Array](../leetcode_questions/421_maximum_xor_of_numbers_in_an_array.md)
- [1707 Maximum XOR with An Element From Array](../leetcode_questions/1707_maximum_xor_with_an_element_from_array.md)