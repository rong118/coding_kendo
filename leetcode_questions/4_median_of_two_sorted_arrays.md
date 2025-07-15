# 4. Median of Two Sorted Arrays

## Question link
(https://leetcode.com/problems/median-of-two-sorted-arrays/)

## Question Description
Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.
The overall run time complexity should be O(log (m+n)).

Example 1:
> Input: nums1 = [1,3], nums2 = [2]
>
> Output: 2.00000
>
> Explanation: merged array = [1,2,3] and median is 2.

Example 2:
> Input: nums1 = [1,2], nums2 = [3,4]
>
> Output: 2.50000
> 
> Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
 
Constraints:
* nums1.length == m
* nums2.length == n
* 0 <= m <= 1000
* 0 <= n <= 1000
* 1 <= m + n <= 2000
* -10^6 <= nums1[i], nums2[i] <= 10^6

## Tags
- array
- divide and conque
- binary search

## Code Implementation
```c++
class Solution {
public:
    double findMedianSortedArrays(vector<int> nums1, vector<int> nums2) {
        int m = nums1.size();
        int n = nums2.size();
        int l = (m + n + 1) / 2;
        int r = (m + n + 2) / 2;
        return (getkth(nums1, 0, nums2, 0, l) + getkth(nums1, 0, nums2, 0, r)) / 2.0;
    }
  
    double getkth(vector<int> nums1, int aStart, vector<int> nums2, int bStart, int k){
        if(aStart == nums1.size()) { return nums2[bStart + k - 1]; }
        if(bStart == nums2.size()) { return nums1[aStart + k - 1]; }
        if(k == 1) return min(nums1[aStart], nums2[bStart]);

        int aMid = INT_MAX;
        int bMid = INT_MAX;
        if(aStart + k/2 - 1 < nums1.size()) aMid = nums1[aStart + k/2 - 1];
        if(bStart + k/2 - 1 < nums2.size()) bMid = nums2[bStart + k/2 - 1];

        if(aMid < bMid){
            return getkth(nums1, aStart + k/2, nums2, bStart, k - k/2);
        }else{
            return getkth(nums1, aStart,       nums2, bStart + k/2, k - k/2);
        }
    }
};
```

## Time Complexity Analysis
> Time complexity  : O(log (m+n))
>
> Space complexity : O(1)
