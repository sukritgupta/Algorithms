# Merge Intervals

**LeetCode:** (56) https://leetcode.com/problems/merge-intervals 
**Difficulty:** Medium  
**Pattern:** Array, Sorting  

---

## Problem Statement
"Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

 

Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
Example 2:

Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
Example 3:

Input: intervals = [[4,7],[1,4]]
Output: [[1,7]]
Explanation: Intervals [1,4] and [4,7] are considered overlapping.
 

Constraints:

1 <= intervals.length <= 104
intervals[i].length == 2
0 <= starti <= endi <= 104"
---

## Intuition


---

## Approach
- Sort the intervals based on first element
- if start of next interval is less than end of previous interval, then increment that interval.    
- In other words, if start of next interval is greater than end of previous interval, push that to results else increment the existing interval in result.

---

## Algorithm
---

## Edge Cases
- Sort can sort a 2D vector based on first value without giving a comparator.
- For vec = {{9,11}, {1,2}, {7,6},} => sort(vec.begin(), vec.end()) works based on sorting first value.
- Also consider scenario {1,3} {4,5}, Ouput should be {1,3} {4,5} and not {1,5} 
---

## C++ Solution
```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        vector<vector<int>> result;
        //Apr1(intervals, result);
        Apr2Optimized(intervals, result);
        return result;
    }

    //Sort the intervals based on first element
    //if start of next interval is less than end of previous interval, then increment that interval.    
    //In other words, if start of next interval is greater than end of previous interval, push that to results else increment the existing interval in result.
    void Apr2Optimized(vector<vector<int>>& intervals, vector<vector<int>>& result){
        sort(intervals.begin(), intervals.end());
        for(const auto& interval: intervals){
            if(result.empty() || result.back()[1] < interval[0]){
                result.push_back(interval);
            }else{
                result.back()[1] = max(result.back()[1], interval[1]);
            }
        }
    }

    //if start of next interval is less than end of previous interval, then increment that interval.
    void Apr1(vector<vector<int>>& intervals, vector<vector<int>>& result){
        //sort intervals
        sort(intervals.begin(), intervals.end(), 
            [&](const auto& interval1, const auto& interval2){return interval1[0] < interval2[0];});
        int start = intervals[0][0];
        int end = intervals[0][1];
        for(int i = 1; i<intervals.size(); ++i){
            int curStart = intervals[i][0];
            int curEnd = intervals[i][1];

            if(start <= curStart && curStart <= end){
                end = max(end, curEnd);
            }else{
                result.push_back({start, end});
                start = curStart;
                end = curEnd;
            }
        }
        result.push_back({start, end});
    }
};
