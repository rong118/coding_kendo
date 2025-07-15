# 287. Find the Duplicate Number

## Question link
(https://leetcode.com/problems/find-the-duplicate-number/)

## Question Description
Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

You must solve the problem without modifying the array nums and uses only constant extra space.

Example 1:
> Input: nums = [1,3,4,2,2]
> 
> Output: 2

Example 2:
> Input: nums = [3,1,3,4,2]
> Output: 3

Example 3:
> Input: nums = [1,1]
>
> Output: 1

Example 4:
> Input: nums = [1,1,2]
>
> Output: 1

Constraints:
- 1 <= n <= 10<sup>5</sup> 
- nums.length == n + 1
- 1 <= nums[i] <= n
- All the integers in nums appear only once except for precisely one integer which appears two or more times.

## Tags
- hashmap
- array
- fast slow pointer

## Code Implementation
```c++
// Running time : O(nlogn)  space : O(1)
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        for(int i = 1; i < nums.size(); i++){
            if(nums[i] == nums[i - 1]){
                return nums[i];
            }
        }
        return -1;
    }
};

// Running time : O(n)  space : O(n)
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        unordered_map<int, int> m;
        for(int i = 0; i < nums.size(); i++){
            m[nums[i]]++;
            if(m[nums[i]] == 2){
                return nums[i];
            }
        }
        return -1;
    }
};

// Running time : O(n) space O(1), Mutate array
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        for(int i = 0; i < nums.size(); i++){
            int index = abs(nums[i]) - 1;
            if(nums[index] > 0){ 
                nums[index] *= -1; 
            }else{
                return index + 1;
            }
        }
        return -1;
    }
};
```


## Fast slow pointer
<img src="../assets/lc287.png" width="400" />

```c++
// Running time : O(n) space O(1), without mutate array
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = nums[0];
        int fast = nums[0];
        while(true){
            slow = nums[slow];
            fast = nums[nums[fast]];
            if(slow == fast){
                fast = nums[0];
                while(fast != slow){
                    slow = nums[slow];
                    fast = nums[fast];
                }
                return slow;
            }
        }
    }
};
```

## Time Complexity Analysis