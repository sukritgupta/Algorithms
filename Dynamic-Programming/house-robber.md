# House Robber

**LeetCode:** (198) https://leetcode.com/problems/house-robber    
**Difficulty:** Medium  
**Pattern:** Dynamic Programming  

---

## Problem Statement
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

 

Example 1:

Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
Example 2:

Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.
 

Constraints:

1 <= nums.length <= 100
0 <= nums[i] <= 400

---

## Intuition


---

## Approach
- We either want to consider max(dp[n-1] , nums[i]+dp[n-2]) as either we are going to consider previous or current +prev2
- Use prev1 and prev2 to avoid extra dp space
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
    int rob(vector<int>& nums) {
        vector<int> dp(nums.size()+1, -1);
        //return max(robRec(nums, 0, dp ), robRec(nums, 1, dp));
        return robTab(nums);
        return robOpt(nums);
    }

    int robOpt(vector<int>& nums) {
        int prev2 = 0, prev1 = 0;

        for (int num : nums) {
            int cur = max(prev1, num + prev2);
            prev2 = prev1;
            prev1 = cur;
        }

        return prev1;
    }

    int robTab(vector<int>& nums, vector<int>& dp) {
        dp[0] = nums[0];
        if(nums.size()>1)
            dp[1] = max(nums[0], nums[1]);

        for(int i=2; i<nums.size(); ++i){
            dp[i] = max(dp[i-1], nums[i] + dp[i-2]);
        }
        return dp[nums.size()-1];
    }

    /* Works But Bad solution*/
    int robRec(vector<int>& nums, int i, vector<int>& dp) {
        int n= nums.size();
        if(i>=n){return 0;}
        if(i==n-1 || i==n-2){return nums[i];}
        if(dp[i] != -1){return dp[i];}
        dp[i] = nums[i] + max(robRec(nums, i+2, dp), robRec(nums, i+3, dp));
        return dp[i];
    }
};
