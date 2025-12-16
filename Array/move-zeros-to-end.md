# Move Zeros

**LeetCode:** (283) https://leetcode.com/problems/move-zeroes    
**Difficulty:** Easy  
**Pattern:** Array  

---

## Problem Statement
Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

 

Example 1:

Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
Example 2:

Input: nums = [0]
Output: [0]
 

Constraints:

1 <= nums.length <= 104
-231 <= nums[i] <= 231 - 1
 

Follow up: Could you minimize the total number of operations done?
---

## Intuition


---

## Approach
- Move all non zeros to left
- keep going right till you find non zero and switch with left
- Left moves when element is switched

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
    void moveZeroes(vector<int>& nums) {
        moveNonZero(nums);    
    }

    //Aproach: Move all non zeros to left
    //keep going right till you find non zero and switch with left
    //Left moves when element is switched
    void moveNonZero(vector<int>& nums){
        int left=0, right = 0;
        for(int right=0; right<nums.size(); ++right){
            if(nums[right] != 0){
                if(left != right){
                    swap(nums[left], nums[right]);
                }
                left++;
            }
        }
    }

    //Two Pointer Approach
    //
    void twoPtr(vector<int>& nums){
        int z=0; int nz =0, n= nums.size();
        if(n<=1){return;}
        while(z < n && nz < n){
            
            while(z<n && nums[z] !=0) {++z;}
            while(nz<z || (nz<n  && nums[nz] ==0)) {++nz;}
            if(z>=n || nz>=n) {break;}
            /*if(z<nz){
                swap(nums[z], nums[nz]);}
            else{
                nz=z;
            }*/
        }
    }

    //Whenever we find a 0, go and find non zero after it and replace
    //Again do it for earlier index of zero +1
    //Possible (n^2 Algo)
    void brute(vector<int>& nums){
        int n = nums.size();
        int i=0;
        while(i <n){
            if(nums[i]==0){
                int j = i+1;
                while(j<n && nums[j] ==0 ){
                    ++j;
                }
                if(j>=n){break;}
                swap(nums[i], nums[j]);
            }
            ++i;
        }
    }
};
