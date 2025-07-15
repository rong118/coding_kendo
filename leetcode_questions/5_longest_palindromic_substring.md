# 5. Longest Palindromic Substring

## Question link
(https://leetcode.com/problems/longest-palindromic-substring/)

## Question Description
Given a string s, return the longest palindromic substring in s.

Example 1:

> Input: s = "babad"
>
> Output: "bab"
>
> Explanation: "aba" is also a valid answer.

   b a b a d
 b 1
 a 1 1
 b 1 1 1
 a 1 1 1 1
 d 1 1 1 1 1


Example 2:

> Input: s = "cbbd"
>
> Output: "bb"

Constraints:
* 1 <= s.length <= 1000
* s consist of only digits and English letters.

## Tags
- string
- dynamic programming

## Code Implementation
```c++
class Solution {
public:     
    string longestPalindrome(string s) {
        vector<vector<int>> dp(s.size(), vector<int>(s.size(), 0));
        int start = 0, end = 0, len = 1;
        for(int i = 0;i < s.size();i++){
            for(int j = 0;j < i + 1;j++){
                dp[i][j] = 1;
            }
        }
        
        for(int i = s.size() - 1;i >= 0;i--){
            for(int j = i + 1;j < s.size();j++){
                if(s[i] == s[j]){
                    dp[i][j] = dp[i + 1][j - 1];
                    if(dp[i][j] == 1 && j -i + 1 > len){
                        len = j - i + 1;
                        start = i;
                        end = j;
                    }
                }else{
                    dp[i][j] = 0;
                }
            }
        }
        
        return s.substr(start,end - start + 1);
    }
};
```

## Time Complexity Analysis
> Time complexity  : O(n^2)
>
> Space complexity : O(n^2)