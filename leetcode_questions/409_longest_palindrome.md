# 409. Longest Palindrome

## Question link
(https://leetcode.com/problems/longest-palindrome/)

## Question Description
Given a string s which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters.

Letters are case sensitive, for example, "Aa" is not considered a palindrome here.

Example 1:

> Input: s = "abccccdd"
>
> Output: 7
>
> Explanation: One longest palindrome that can be built is "dccaccd", whose length is 7.

Example 2:

> Input: s = "a"
> 
> Output: 1
>
> Explanation: The longest palindrome that can be built is "a", whose length is 1.

Constraints:
* 1 <= s.length <= 2000
* s consists of lowercase and/or uppercase English letters only.

## 分类
- string
- hashMap

## Code Implementation
```c++
class Solution {
public:
    int longestPalindrome(string s) {
        unordered_map<char,int> map;
        int ans = 0;
        int odd = 0;
        
        for(auto i : s){
            map[i]++;
        }
        
        for(auto j = map.begin();j!=map.end();j++){
            if(j->second % 2==0){
                ans += j->second;
            }else{
                odd = 1;
                ans += j->second - 1;
            }
        }

        return ans + odd;
    }
};
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(n)