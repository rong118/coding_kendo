# 3. Longest Substring Without Repeating Characters

## Question link
(https://leetcode.com/problems/longest-substring-without-repeating-characters/)

## Question Description
Given a string s, find the length of the longest substring without repeating characters.

Example 1:

> Input: s = "abcabcbb"
>
> Output: 3
>
> Explanation: The answer is "abc", with the length of 3.

Example 2:

> Input: s = "bbbbb"
>
> Output: 1
>
> Explanation: The answer is "b", with the length of 1.

Example 3:

> Input: s = "pwwkew"
>
> Output: 3
>
> Explanation: The answer is "wke", with the length of 3.
>
> Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
 

Constraints:
- 0 <= s.length <= 5 * 10^4
- s consists of English letters, digits, symbols and spaces.

## Tags
- string
- sliding window
- hashMap

## Code Implementation
```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if(s.size() == 0) { return 0; }
        vector<int> m(256, 0);
        int l = 0;
        int r = 0;
        int ans = 1;
        
        while(r < s.size()){
            m[s[r]] += 1;
            while(m[s[r]] > 1){
                m[s[l]]--;
                l++;
            }
            ans = max(ans, r - l + 1);
            r++;
        }

        return ans;
    }
};
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)