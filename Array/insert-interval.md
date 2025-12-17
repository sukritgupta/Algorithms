# Insert Interval

**LeetCode:** (121) https://leetcode.com/problems/insert-interval   
**Difficulty:** Medium  
**Pattern:** Array  

---

## Problem Statement
You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.

Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return intervals after the insertion.

Note that you don't need to modify intervals in-place. You can make a new array and return it.

 

Example 1:

Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
Example 2:

Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
 

Constraints:

0 <= intervals.length <= 104
intervals[i].length == 2
0 <= starti <= endi <= 105
intervals is sorted by starti in ascending order.
newInterval.length == 2
0 <= start <= end <= 105
---

## Intuition
- Just a variation of Merge interval.
---

## Approach 1(Leetcode)
- In a new list:
- Add all the elemnents before merge is needed
- Merge the newInterval with all the succedding intervals which can be merged and add the final interval to list.
- Add remaining intervals
## Approach 2  
- Decide which interval needs to be added(newInterval/ next interval) and merge it into exisitng result list, using merge interval.
---

## Algorithm
---

## Edge Cases
- Remember that now we need insert n+1 elements in list.
- Beware about using correct indexes.
---

## C++ Solution
```cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals,
                               vector<int>& newInterval) {
        bool newIntervalAdded = 0;
        vector<vector<int>> mergedIntervals;
        for (int i = 0; i < intervals.size();) {
            vector<int> interval = intervals[i];
            vector<int> intervalToPush;
            if (!newIntervalAdded && newInterval[0] < interval[0]) {
                intervalToPush = newInterval;
                newIntervalAdded = 1;
            } else {
                intervalToPush = interval;
                ++i;
            }
            mergeInterval(mergedIntervals, intervalToPush);
        }
        if (!newIntervalAdded) {
            mergeInterval(mergedIntervals, newInterval);
        }
        return mergedIntervals;
    }

    void mergeInterval(vector<vector<int>>& mergedIntervals,
                       const vector<int>& intervalToPush) {
        if (mergedIntervals.empty() ||
            mergedIntervals.back()[1] < intervalToPush[0]) {
            mergedIntervals.push_back(intervalToPush);
        } else {
            mergedIntervals.back()[1] =
                max(mergedIntervals.back()[1], intervalToPush[1]);
        }
    }
};
