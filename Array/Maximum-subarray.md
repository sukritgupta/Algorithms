# Maximum SubArray

**LeetCode:** (53) https://leetcode.com/problems/maximum-subarray  
**Difficulty:** Medium  
**Pattern:** Array, DP, Kadane  
**Revision Needed:** Yes, Unable to solve in first attempt

---

## Problem Statement
Given an integer array nums, find the subarray with the largest sum, and return its sum.

 

Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.
Example 2:

Input: nums = [1]
Output: 1
Explanation: The subarray [1] has the largest sum 1.
Example 3:

Input: nums = [5,4,-1,7,8]
Output: 23
Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.
 

Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104
 

Follow up: If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

---

## Intuition


---

## Approach 1:(Kadane)
The sum of the current sub array is only beneficial till the time it is +ve. Even if it is just +1, it is going to add some value to further numbers.  
Once it becomes negative, maximum till here is already recorded and this sum is no longer useful for next numbers.
Keep 2 variables `curSum` and `maxSum`.  
- curSum is sum of all the numbers till now.  
- maxSum is max of all the sums till now.  
- Whenever curSum gets negative, reset it to 0.   

## Approach 2: (Divide and conquer)
**Getting Difficulty understanding it.**
Find max of left side, max of right side, and the max sum of current subarray with ith num in middle and return maximum amongst these.
1. Exit condition: if left > right, return INT_MIN
2. Consider 3 elements
   a. Find Max of left.
   b. Find Max of right.
   c. Find current max possible by calculating the max contigous sum possible on left, max contigous sum possible on right, and adding mid element to it.
   d. Return max of above 3.
---

## Algorithm
---

## Edge Cases
---

## C++ Solution
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        //return resetWhenNeg(nums);
        return DC(nums, 0, nums.size()-1);
    }

    int resetWhenNeg(vector<int>& nums) {
        int maxSum = nums[0];
        int curSum = 0;
        for(int i=0; i<nums.size();++i){
            curSum += nums[i];
            maxSum = max(maxSum, curSum);
            curSum = max(curSum, 0); 
        }
        return maxSum;
    }

    int DC(vector<int>& nums, int l, int r) {
        if(l>r)
            return INT_MIN;

        int m = (l+r)/2;
        int ml = DC(nums, l, m-1);
        int mr = DC(nums, m+1, r);
        int sum = 0;
        int sumL=0, sumR=0;

        //find the max possible sum of contigous elements on left
        for(int i=m-1; i>=l; --i){
            sum+= nums[i];
            sumL = max(sumL, sum);
        }
        sum = 0;
        //find the max possible sum of contigous elements on right
        for(int i=m+1; i<=r; ++i){
            sum+= nums[i];
            sumR = max(sumR, sum);
        }

        return max(max(ml,mr), sumL+sumR+nums[m]);
    }
};
