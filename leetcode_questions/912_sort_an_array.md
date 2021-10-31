# 912. Sort an Array

## Question link
> (https://leetcode.com/problems/sort-an-array/)

## Question Description
Given an array of integers nums, sort the array in ascending order.

Example 1:
> Input: nums = [5,2,3,1]
> Output: [1,2,3,5]

Example 2:
> Input: nums = [5,1,1,2,0,0]
> Output: [0,0,1,1,2,5]

Constraints:
1 <= nums.length <= 5 * 10<sup>4</sup> 
-5 * 10<sup>4</sup>  <= nums[i] <= 5 * 10<sup>4</sup> 

## 分类 && 解题思路
- heap sort

## Code Implementation
```c++
class Solution {
public:
    vector<int> sortArray(vector<int>& arr) {
        int n = arr.size();

        // Build heap
        for(int i = n/2; i >= 0; i--){
            heapify(arr, n, i);
        }

        // One by one extract from heap
        for(int i = n - 1; i > 0 ;i--){
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;
            heapify(arr, i, 0);
        }
        
        return arr;
        
    }
    
    void heapify(vector<int>& arr, int n, int i){
        int largest = i;
        int l = 2 * i + 1;
        int r = 2 * i + 2;

        // If left child is larger than root
        if(l < n && arr[l] > arr[largest]){
            largest = l;
        }

        // If right child is larger than root
        if(r < n && arr[r] > arr[largest]){
            largest = r;
        }

        // If largest is not root
        if(largest != i){
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            heapify(arr, n, largest);
        }
    }
};
```

## Time Complexity Analysis
Running time  : O(n)