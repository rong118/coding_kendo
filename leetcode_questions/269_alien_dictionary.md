# 269. Alien Dictionary

## Question link
(https://leetcode.com/problems/alien-dictionary/)

## Question Description
There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of non-empty words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

<br/>

Example 1:
> Given the following words in dictionary,
>
> [
>  "wrt",
>  "wrf",
>  "er",
>  "ett",
>  "rftt"
> ]
>
> The correct order is: "wertf".

Example 2:
> Given the following words in dictionary,
>
> [
>  "z",
>  "x"
> ]
>
> The correct order is: "zx".

Example 3:
> Given the following words in dictionary,
>
> [
>  "z",
>  "x",
>  "z"
> ]
>
> The order is invalid, so return "".


Note:
- You may assume all letters are in lowercase.
- You may assume that if a is a prefix of b, then a must appear before b in the given dictionary.
- If the order is invalid, return an empty string.
- There may be multiple valid order of letters, return any one of them is fine.

<br/>

## 分类 && 解题思路
- graph
- topologic sort

## Code Implementation
```c++
// bfs topologic sort
class solution {
    unordered_map<char, vector<char>> g;
    unordered_map<char, int> indegree;
    bool valid = true;
    string alienOrder(vector<string> words){
        _build(words);
        if(valid == false) return "";

        string sb;
        deque<char> q;
        // 入度
        for(auto k = indegree.begin(); k != indegree.end(); k++){
            if(k.second == 0){
                q.push_back(k.first);
            }
        }

        // topologic
        while(!q.empty()){
            char c = q.front(); q.pop_front();
            s += c;
            for(char nei : g[c]){
                indregee[nei]--;
                if(indregee[nei] == 0) q.push_back(nei);
            }
        }

        return sb.size() < indegree.size() ? "" : sb;
    }

    void _build(vector<string> words){
        // build graph and indgree
        for(string word : words){
            for(char c : word){
                indegree[c] = 0;
                g[c] = {};
            }
        }

        for(int i = 0; i < words.size() - 1; i++){
            string word1 = words[i];
            string word2 = words[i + 1];
            if(word1.size() > word2.size() && word1.find(word2, 0) == 0) valid = false;
            
            for(int j = 0; j < min(word1.size(), word2.size()); j++){
                if(word1[j] != word2[j]){
                    g[word1[j]].push_back(word2[j]);
                    indegree[word2[j]] = indegree[word1[j]] + 1;
                    break;
                }
            }
        }
    }
}
```

## Time Complexity Analysis