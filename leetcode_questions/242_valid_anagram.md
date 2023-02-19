# 242. Valid Anagram

## Question link
(https://leetcode.com/problems/valid-anagram/)

## Question Description
GGiven two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

> Input: s = "anagram", t = "nagaram"
>
> Output: true

Example 2:

> Input: s = "rat", t = "car"
>
> Output: false
 

Constraints:

* 1 <= s.length, t.length <= 5 * 104
* s and t consist of lowercase English letters.

## 分类
- string
- hashMap

## Code Implementation
```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.size() != t.size()) return false;
        vector<int> map(256, 0);
        
        for(int i = 0;i < s.size();i++){
            map[s[i]]++;
        }
        
        for(int i = 0;i < t.size();i++){
            if(map[t[i]] <= 0) 
                return false;
            else{
                map[t[i]]--;
            }
        }
        
        return true;
    }
};
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)