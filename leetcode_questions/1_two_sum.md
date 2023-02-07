# 1. Two Sum

## Question link
(https://leetcode.com/problems/two-sum/)

## Question Description
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Example 1:
> Input: nums = [2,7,11,15], target = 9
>
> Output: [0,1]
>
> Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:
> Input: nums = [3,2,4], target = 6
>
> Output: [1,2]

Example 3:
> Input: nums = [3,3], target = 6
>
> Output: [0,1]

Constraints:
* 2 <= nums.length <= 10^4
* -10^9 <= nums[i] <= 10^9
* -10^9 <= target <= 10^9
* Only one valid answer exists.

## 分类 && 解题思路
- Array
- Sort
- HashMap

## Code Implementation
```c++
class Solution{
public:
    vector<int> twoSum(vector<int> &numbers, int target){
        vector<int> output;
        map<int,int> m;
        int findValue;
        for(int i = 0; i < numbers.size(); i++){
            findValue = target - numbers[i];
            if(m.find(findValue) == m.end()){
                m[numbers[i]] = i;
            }else{
                output.push_back(m[findValue]);
                output.push_back(i);
            }
        }
        return output;
    }
};
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(n)