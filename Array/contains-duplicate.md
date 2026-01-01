# Contains Duplicate

**LeetCode:** (217) https://leetcode.com/problems/contains-duplicate  
**Difficulty:** Easy  
**Pattern:** Array  

---

## Problem Statement
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

 

Example 1:

Input: nums = [1,2,3,1]

Output: true

Explanation:

The element 1 occurs at the indices 0 and 3.

Example 2:

Input: nums = [1,2,3,4]

Output: false

Explanation:

All elements are distinct.

Example 3:

Input: nums = [1,1,1,3,3,4,3,2,4,2]

Output: true

 

Constraints:

1 <= nums.length <= 105
-109 <= nums[i] <= 109
---

## Intuition


---

## Approach
Keep Putting elements in a set and check if it already exists
---

## Key Insights
---

## Mistakes
---

## Edge Cases
---

## C++ Solution
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> counter;
        for(const int num:nums){
            if(counter.count(num)) return true;
            counter.insert(num); 
        }
        return false;
    }
};
