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
- Find sum of left side, right side, and all the current numbers and return maximum.
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
        return kadane(nums);
    }

    int kadane(vector<int>& nums) {
        int maxSum = nums[0];
        int curSum = 0;
        for(int i=0; i<nums.size();++i){
            curSum += nums[i];
            maxSum = max(maxSum, curSum);
            curSum = max(curSum, 0); 
        }
        return maxSum;
    }
};
