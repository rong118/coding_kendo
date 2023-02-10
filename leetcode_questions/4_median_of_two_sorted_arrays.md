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

## 分类
- array
- divide and conque
- binary search


## Code Implementation
```c++
class solution {
public:
  double findMedianSortedArrays(vector<int> nums1, vector<int> nums2) {
    int m = nums1.size();
    int n = nums2.size();
    int l = (m + n + 1) / 2;
    int r = (m + n + 2) / 2;
    return (getkth(nums1, 0, nums2, 0, l) + getkth(nums1, 0, nums2, 0, r))) / 2.0;
  }
  
  double getkth(vector<int> nums1, int aStart, vector<int> nums2, int bStart, int k){
    if(aStart == nums1.size()) { return B[bStart + k - 1]; }
    if(bStart == nums2.size()) { return A[aStart + k - 1]; }
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
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;
        
        if((m+n)%2==0){
            return (findMedian(nums1, m, nums2, n, (m+n)/2) + findMedian(nums1, m, nums2, n, (m+n)/2+1))/2.0; 
        }else{
            return findMedian(nums1, m, nums2, n, (m+n)/2+1);
        }
    }
    
    //O(lg(m+n))
    int findMedian(int[] a, int m, int[] b,  int n, int k){
        if (m <= 0) return b[k-1];  
        if (n <= 0) return a[k-1];  
        if (k <= 1) return Math.min(a[0], b[0]);   
        
        if (b[n/2] >= a[m/2]){  
             if ((n/2 + 1 + m/2) >= k)  
                  return findMedian(a, m, b, n/2, k);  
             else {
                  int[] copy_a = new int[m - (m/2 + 1)];
                  System.arraycopy( a, m/2 + 1, copy_a, 0, m - (m/2 + 1) );
                  return findMedian(copy_a, m - (m/2 + 1), b, n, k - (m/2 + 1));  
             }
        }else{  
             if ((m/2 + 1 + n/2) >= k)  
                  return findMedian( a, m/2,b, n, k);  
             else  {
                  int[] copy_b = new int[n - (n/2 + 1)];
                  System.arraycopy( b, n/2 + 1, copy_b, 0, n - (n/2 + 1) );
                  return findMedian( a, m, copy_b, n - (n/2 + 1), k - (n/2 + 1));
             }
        }
    }

}
```

## Time Complexity Analysis
> Time complexity  : O(log (m+n))
>
> Space complexity : O(n)
