# 125. Valid Palindrome

## Question link
(https://leetcode.com/problems/valid-palindrome/)

## Question Description
A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

Example 1:

> Input: s = "A man, a plan, a canal: Panama"
> 
> Output: true
>
> Explanation: "amanaplanacanalpanama" is a palindrome.

Example 2:

> Input: s = "race a car"
>
> Output: false
>
> Explanation: "raceacar" is not a palindrome.

Example 3:

> Input: s = " "
>
> Output: true
> Explanation: s is an empty string "" after removing non-alphanumeric characters.
> Since an empty string reads the same forward and backward, it is a palindrome.
 

Constraints:

* 1 <= s.length <= 2 * 10^5
* s consists only of printable ASCII characters.

## Tags
- string

## Code Implementation
```c++
class Solution {
public:
    bool isPalindrome(string s) {
        int l = 0;
        int r = s.size() - 1;
        while(l < s.size() && r >= 0 && l < r){
            if(!isalnum(s[l])){ l++; continue; }
            if(!isalnum(s[r])){ r--; continue; }
            if(std::tolower(s[l++]) != std::tolower(s[r--])){
                return false;
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