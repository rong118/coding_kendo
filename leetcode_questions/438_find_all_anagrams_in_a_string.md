# 438. Find All Anagrams in a String

## Question link
(https://leetcode.com/problems/find-all-anagrams-in-a-string/)

## Question Description
Given two strings s and p, return an array of all the start indices of p's anagrams in s. You may return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

> Input: s = "cbaebabacd", p = "abc"
> 
> Output: [0,6]
>
> Explanation:
>
> The substring with start index = 0 is "cba", which is an anagram of "abc".
>
> The substring with start index = 6 is "bac", which is an anagram of "abc".

Example 2:

> Input: s = "abab", p = "ab"
>
> Output: [0,1,2]
>
> Explanation:
> The substring with start index = 0 is "ab", which is an anagram of "ab".
>
> The substring with start index = 1 is "ba", which is an anagram of "ab".
>
> The substring with start index = 2 is "ab", which is an anagram of "ab".
 

Constraints:
* 1 <= s.length, p.length <= 3 * 10^4
* s and p consist of lowercase English letters.

## 分类
- string
- hashMap

## Code Implementation
```c++
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        // Initial p ino map;
        vector<int> m(26, 0);
        for(char c : p){
            m[c - 'a']++;
        }

        // Sliding Windows
        vector<int> ans;
        int tmp = 0;
        vector<int> tm(26, 0);
        int l = 0;
        int r = 0;
        
        while(r < s.size()){
            if(m[s[r] - 'a'] > 0){
                tm[s[r] - 'a']++;
                if(_same(m, tm)){
                    ans.push_back(l);
                }
            }else{
                _reset(tm);
                l = r + 1;
            }
            r++;
            if(r - l + 1 > p.size()){
                tm[s[l] - 'a'] --;
                l++;
            }
        }

        return ans;
    }

    void _reset(vector<int> &a){
        for(int i = 0; i < a.size(); i++){
            a[i] = 0;
        }
        return;
    }
    bool _same(vector<int> &a, vector<int> &b){
        if(a.size() != b.size()) {return false;}
        for(int i = 0; i < a.size(); i++){
            if(a[i] != b[i]){
                return false;
            }
        }
        return true;
    }
};

class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int> res;
        int hash[256] ={0}; //character hash
        
        for (auto c : p) {
            hash[c]++;
        }
        
        //two points, initialize count to p's length
        int left = 0, right = 0, count = p.length();
        while (right < s.size()) {
            //move right everytime, if the character exists in p's hash, decrease the count
            //current hash value >= 1 means the character is existing in p
            if (hash[s[right]] >= 1) {
                count--; 
            }
            hash[s[right]]--;
            right++;
            
            
            //when the count is down to 0, means we found the right anagram
            //then add window's left to result list
            if (count == 0) {
                res.push_back(left);
            }
            
            //if we find the window's size equals to p, then we have to move left (narrow the window) to find the new match window
            //++ to reset the hash because we kicked out the left
            //only increase the count if the character is in p
            //the count >= 0 indicate it was original in the hash, cuz it won't go below 0
            if (right - left == p.length()){
                if(hash[s[left]] >= 0) {
                    count++;
                }
                hash[s[left]]++;   
                left++;
            }
            
        }
        
        return res;
    }
};
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)