# 76. Minimum Window Substring

## Question link
(https://leetcode.com/problems/minimum-window-substring/)

## Question Description
Given two strings s and t of lengths m and n respectively, return the minimum window 
substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

Example 1:

> Input: s = "ADOBECODEBANC", t = "ABC"
> 
> Output: "BANC"
>
> Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

Example 2:

> Input: s = "a", t = "a"
>
> Output: "a"
>
> Explanation: The entire string s is the minimum window.

Example 3:

> Input: s = "a", t = "aa"
>
> Output: ""
>
> Explanation: Both 'a's from t must be included in the window.
>
> Since the largest window of s only has one 'a', return empty string.
 

Constraints:
* m == s.length
* n == t.length
* 1 <= m, n <= 10^5
* s and t consist of uppercase and lowercase English letters.


## 分类
- string
- sliding window

## Code Implementation
```c++
class Solution {
public:
    string minWindow(string s, string t) {
        vector<int> m(256, 0);
        for(char c : t){
            m[c]++;
        }

        int cnt = t.size();
        int l = 0;
        int r = 0;
        int ans = INT_MAX;
        string res = "";
        while(r < s.size()){
            if(m[s[r]] > 0){
                cnt--;
            }
            m[s[r]]--;
            r++;
            while(cnt == 0){
                if(ans > r - l + 1) {
                    ans = r - l + 1;
                    res = s.substr(l, r - l + 1);
                }

                if(m[s[l]] >= 0){ // m[s[l]] >= 0 means s[l] is included in t
                    cnt++;
                }
                m[s[l]]++;
                l++;
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