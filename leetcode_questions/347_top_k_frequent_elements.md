# 347. Top K Frequent Elements

## Question link
> link

## Question Description
Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

Example 1:

> Input: nums = [1,1,1,2,2,3], k = 2
> Output: [1,2]

Example 2:

> Input: nums = [1], k = 1
> Output: [1]


Constraints:

1 <= nums.length <= 10<sup>5</sup>
k is in the range [1, the number of unique elements in the array].
It is guaranteed that the answer is unique.

## 分类 && 解题思路
- heap

## Code Implementation
```c++
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        // O(1) time
        if (k == nums.size()) {
            return nums;
        }

        // 1. build hash map : element and how often it appears
        // O(N) time
        unordered_map<int, int> count_map;
        for (int n : nums) {
            count_map[n] += 1;
        }

        // initialise a heap with most frequent elements at the top
        auto comp = [&count_map](int n1, int n2) { return count_map[n1] > count_map[n2]; };
        priority_queue<int, vector<int>, decltype(comp)> heap(comp);

        // 2. keep k top fequent elements in the heap
        // O(N log k) < O(N log N) time
        for (pair<int, int> p : count_map) {
            heap.push(p.first);
            if (heap.size() > k) heap.pop();
        }

        // 3. build an output array
        // O(k log k) time
        vector<int> top(k);
        for (int i = k - 1; i >= 0; i--) {
            top[i] = heap.top();
            heap.pop();
        }
        return top;
    }
};
```

## Time Complexity Analysis
Running time  :   O(nlog(K))
Space complexity : O(N + k)