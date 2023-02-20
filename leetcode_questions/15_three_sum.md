# 15. 3Sum

## Question link
(https://leetcode.com/problems/3sum/)

## Question Description
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

Example 1:

> Input: nums = [-1,0,1,2,-1,-4]
>
> Output: [[-1,-1,2],[-1,0,1]]
>
> Explanation: 
> nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
>
> nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
>
> nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
>
> The distinct triplets are [-1,0,1] and [-1,-1,2].
>
> Notice that the order of the output and the order of the triplets does not matter.

Example 2:

> Input: nums = [0,1,1]
>
> Output: []
>
> Explanation: The only possible triplet does not sum up to 0.

Example 3:

> Input: nums = [0,0,0]
>
> Output: [[0,0,0]]
>
> Explanation: The only possible triplet sums up to 0.
 

Constraints:

* 3 <= nums.length <= 3000
* -10^5 <= nums[i] <= 10^5

## 分类
- array
- sort
- two pointers

## Code Implementation
```c++
class Solution {
public:
    vector<vector<int> > threeSum(vector<int> &num) {
        vector<vector<int> > out;
        sort(num.begin(), num.end());
        int size = num.size();
        
        for(int i = 0;i < size;i++){
            if(i == 0 || num[i] != num[i - 1]){
                _twoSum(num, num[i], i, out);
            }
        }
        
        return out;
    }

    // two pointer
    void _twoSum(vector<int> &numbers, int target, int start, vector<vector<int> > &out){
        int left = start + 1;
        int right = numbers.size() - 1;
        
        while(left < right){
            if(numbers[left] + numbers[right] + target == 0){
                out.push_back({target, numbers[left], numbers[right]});
                while(left < right && numbers[left] == numbers[left + 1]) left++;
                left++;
                while(left < right && numbers[right] == numbers[right - 1]) right--;
                right--;
            }else if(numbers[left] + numbers[right] + target < 0){
                left++;
            }else{
                right--;
            }
        }
    }
};
```

## Time Complexity Analysis
> Time complexity  : O(n^2)
>
> Space complexity : O(n)