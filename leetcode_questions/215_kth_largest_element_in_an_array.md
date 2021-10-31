# 215. Kth Largest Element in an Array

## Question link
> (https://leetcode.com/problems/kth-largest-element-in-an-array/)

## Question Description
Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

Example 1:
> Input: nums = [3,2,1,5,6,4], k = 2
> Output: 5

Example 2:
> Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
> Output: 4

Constraints:
1 <= k <= nums.length <= 10<sup>4</sup> 
-10<sup>4</sup>  <= nums[i] <= 10<sup>4</sup> 

## 分类 && 解题思路

## Code Implementation
```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        unordered_map<int, int> count_map;
        for (int n : nums) {
            count_map[n]++;
        }

        // initialise a heap with most frequent elements at the top
        auto comp = [](int n1, int n2) { return n1 > n2; };
        priority_queue<int, vector<int>, decltype(comp)> heap(comp);

        // 2. keep k top largest elements in the heap
        // O(N log k)
        for (auto p : count_map) {            
            for(int i = 0; i < count_map[p.first]; i++){
                heap.push(p.first);
                if (heap.size() > k) {
                    // cout<<"pop " << heap.top()<<endl;
                    heap.pop();
                }
            }
        }

        return heap.top();
    }
};
```

## Time Complexity Analysis
Running time  : O(nlog(k))