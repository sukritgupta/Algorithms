# 3Sum

**LeetCode:** (15) https://leetcode.com/problems/3sum  
**Difficulty:** Medium  
**Pattern:** Array 2 Pointer, Sort  

---

## Problem Statement
---

## Intuition
- Fix `i` + 2 pointer

---

## Approach
Fix `i` + 2 pointer
- Move `i` for all locations. For each `i`, move `j` and `k`.
- If sum is 0, push and j++ else move two pointer(j,k) as per sum.
- For no Duplicates, skip i and j, if they are equal to prev num, after checking them once.    
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
    vector<vector<int>> threeSum(vector<int>& nums) {
        return Appr1(nums);
    }

    vector<vector<int>> Appr1(vector<int>& nums){
        vector<vector<int>> result;
        sort(nums.begin(), nums.end());
        int i=0;
        for(int i=0; i<nums.size(); ++i){ //prevent duplicate
            if(i>0 && nums[i-1]==nums[i]){
                continue;
            }
            int j=i+1, k=nums.size()-1;
            while(j<k){
                if(j>i+1 && nums[j-1]==nums[j]){ //prevent duplicate
                    j++;
                    continue;
                }
                if(nums[i]+nums[j]+nums[k] == 0){
                    result.push_back({nums[i], nums[j], nums[k]});
                    j++;
                }else if(nums[i]+nums[j]+nums[k]>0){
                        k--;
                }else{
                    j++;
                }
            }
        }
        return result;
    }
};
