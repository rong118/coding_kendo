# 56. Merge Intervals

## Question link
(https://leetcode.com/problems/merge-intervals/)

## Question Description
Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

Example 1:

> Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
>
> Output: [[1,6],[8,10],[15,18]]
>
> Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

Example 2:

> Input: intervals = [[1,4],[4,5]]
>
> Output: [[1,5]]
>
> Explanation: Intervals [1,4] and [4,5] are considered overlapping.
 
Constraints:

- 1 <= intervals.length <= 10^4
- intervals[i].length == 2
- 0 <= starti <= endi <= 10^4

## Tags
- Array
- Sort

## Code Implementation
```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ans;
        vector<int> cur = intervals[0];
        for(int i = 1; i < intervals.size(); i++){
            if(intervals[i][1] <= cur[1]){
                // Do nothing
            }else{
                if(intervals[i][0] > cur[1]){
                    ans.push_back(cur);
                    cur = intervals[i];
                }else{
                    cur[1] = intervals[i][1];
                }
            }
        }

        //push last cur into ans
        ans.push_back(cur);

        return ans;
    }
};
```

## Time Complexity Analysis
> Time complexity  : O(nlog(n))
>
> Space complexity : O(n)