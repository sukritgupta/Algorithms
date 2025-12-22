# Subsets

**LeetCode:** (78) https://leetcode.com/problems/subsets/description/  
**Difficulty:** Medium  
**Pattern:** Array, BackTracking  

---

## Problem Statement
Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

 

Example 1:

Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
Example 2:

Input: nums = [0]
Output: [[],[0]]
 

Constraints:

1 <= nums.length <= 10
-10 <= nums[i] <= 10
All the numbers of nums are unique.
---

## Intuition


---

## Approach 1 (Iterative)
- Start res with {}, and for each num, add num to all res elements till now and add all of them to res.
- ex: {}, Add 1 => {},, {1}, For 2 => {},{1} ,, {2}, {1,2} 
## Approach 2(BackTracking)(complexity: 2^n)
Back Tracking with for Loop
- Push current path then add all possible nums for each num...
- General BackTracking Idea:
  - Push num to Path, Process Num, Pop Num from Path
---

## Key Insights
---

## Mistakes
---

## Edge Cases
---

## C++ Solution
```cpp
