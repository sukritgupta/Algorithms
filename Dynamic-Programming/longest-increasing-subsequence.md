# Longest Increasing Subsequence

**LeetCode:** (300) https://leetcode.com/problems/longest-increasing-subsequence  
**Difficulty:** Medium  
**Pattern:** DP, Array, Sort  

---

## Problem Statement
"Given an integer array nums, return the length of the longest strictly increasing subsequence.

 

Example 1:

Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
Example 2:

Input: nums = [0,1,0,3,2,3]
Output: 4
Example 3:

Input: nums = [7,7,7,7,7,7,7]
Output: 1
 

Constraints:

1 <= nums.length <= 2500
-104 <= nums[i] <= 104
 

Follow up: Can you come up with an algorithm that runs in O(n log(n)) time complexity?"
---

## Intuition


---

## Approach 1(Recursion 2D DP)
> This approach looks to the right and asks:  
> “What is the LIS starting from here, given my previous choice?” 
- Find LIS after the current number. Here we consider right of cur num
- Either we don't take an element and procced to next
- or we take it if it is greater than prev.
- Take max of above to find LIS
- We need to take 2D array for dp as our answer depends on prev and curr num
## Approach 2: Tabulation(1D DP)
> “If I **must end** at i, what is the best LIS I can form?”
- Concept: Find LIC for window ending at current num. Here we are considering left of cur num.
- For each num, find the max LIC on its left and add 1.
## Approach 3: Greedy + Binary Sort O(nlogn)
- Create a sorted vector of needed sequence.
- Find the just >= of cur num in vec and replace it, else add num
- Replace if `lower_bound`(binary search) available else add to vector.
> The vector is NOT the actual LIS. It only helps compute the length  
> Why replacement works: Smaller tail = more chances to extend later

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

    int lengthOfLIS(vector<int>& nums) {
        return   lengthOfLISGreedyBinary(nums);      
        //return lengthOfLISItr(nums);

        //vector<vector<int>> dp(nums.size(), vector<int>(nums.size()+1, -1));
        //return lengthOfLISRec(nums, 0, -1, dp);
    }

    int lengthOfLISGreedyBinary(vector<int>& nums) {
        vector<int> tail;
        for(auto num: nums){
            auto itr = lower_bound(tail.begin(), tail.end(), num);
            if(itr == tail.end()){
                tail.emplace_back(num);
            }else{
                *itr = num;
            }
        }
        return tail.size();
    }

    int lengthOfLISItr(vector<int>& nums) {
        vector<int> dp(nums.size(),1);
        for(int idx = 1; idx<nums.size(); ++idx){
            for(int prev = 0; prev<idx; ++prev){
                if(nums[idx] > nums[prev]){
                    dp[idx] = max(dp[idx], 1 + dp[prev]);
                }
                
            }
        }
        return *max_element(dp.begin(), dp.end());
    }

    int lengthOfLISRec(vector<int>& nums, int idx, int prev, vector<vector<int>>& dp) {
        if(idx == nums.size()){
            return 0;
        }
        if(dp[idx][prev+1] != -1){
            return dp[idx][prev+1];
        }

        int tk = 0;
        int nt  = lengthOfLISRec(nums, idx+1, prev, dp);
        if(prev == -1 || nums[idx] > nums[prev]){
            tk  = 1 + lengthOfLISRec(nums, idx+1, idx, dp);
        }
        dp[idx][prev+1] = max(tk, nt);
        return dp[idx][prev+1];
    }
};
