# Permutations

**LeetCode:** (46) https://leetcode.com/problems/permutations  
**Difficulty:** Medium  
**Pattern:** Array, Backtracking  

---

## Problem Statement
"Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

 

Example 1:

Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
Example 2:

Input: nums = [0,1]
Output: [[0,1],[1,0]]
Example 3:

Input: nums = [1]
Output: [[1]]
 

Constraints:

1 <= nums.length <= 6
-10 <= nums[i] <= 10
All the integers of nums are unique."

---

## Intuition


---

## Approach
"Time=>O(n*n!)  
Apr1: Add a num to path, recurse, pop path. Add path.length ==nums.size, add to res. Requires extra space to store elements which are already used.  

Apr2: Fix a position and swap it with all numbers. Elems before fixed pos are fixed. Add when index = = nums.size()"  

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
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> path;
        vector<bool> used(nums.size(), false);
        
        permuteRec(nums, path, res, used);
        //permuteSwap(nums, res, 0);
        return res;

    }

    void permuteSwap(vector<int>& nums, 
                                     vector<vector<int>>& res,  int ind) {
        if(ind == nums.size()){
            res.emplace_back(nums);
            return;
        }

        for(int i=ind; i<nums.size(); ++i){
            swap(nums[i], nums[ind]);
            permuteSwap(nums, res, ind+1);
            swap(nums[i], nums[ind]);
        }
    }

    void permuteRec(vector<int> nums, vector<int>& path,
                                     vector<vector<int>>& res,  vector<bool>& used) {
        if(path.size()==nums.size()){
            res.emplace_back(path);
            return;
        }
        for(int i=0; i<nums.size(); ++i){
            if(!used[i]){
                path.emplace_back(nums[i]);
                used[i] = true;
                permuteRec(nums, path, res, used);
                path.pop_back();
                used[i] = false;
            }
        }
    }
};
