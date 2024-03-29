# 169. Majority Element

## Question link
(https://leetcode.com/problems/majority-element/description/)

## Question Description
Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. 

You may assume that the majority element always exists in the array.

Example 1:

> Input: nums = [3,2,3]
>
> Output: 3

Example 2:

> Input: nums = [2,2,1,1,1,2,2]
>
> Output: 2

Constraints:

- n == nums.length
- 1 <= n <= 5 * 104
- -109 <= nums[i] <= 109

## 分类
- Array

## Code Implementation
```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int n;
        int c = 0;
        
        for(int num: nums){
            if(n == num){
                c++;
            }else if(c == 0){
                n = num;
                c++;
            }else
                c--;
        }
        
        return n;
    }
};
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)