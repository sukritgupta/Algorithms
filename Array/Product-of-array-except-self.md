# Name

**LeetCode:** (238) https://leetcode.com/problems/product-of-array-except-self    
**Difficulty:** Medium  
**Pattern:** Array, Prefix Sum  

---

## Problem Statement  
Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

 

Example 1:

Input: nums = [1,2,3,4]
Output: [24,12,8,6]
Example 2:

Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
 

Constraints:

2 <= nums.length <= 105
-30 <= nums[i] <= 30
The input is generated such that answer[i] is guaranteed to fit in a 32-bit integer.
 

Follow up: Can you solve the problem in O(1) extra space complexity? (The output array does not count as extra space for space complexity analysis.)  

---

## Intuition
- We need to separately calculate the product of left and right elements. 

---

## Approach 1: (Using 2 extra arrays:: leftRightProd()) (Space: O(2n), Time: O(n))
1. In One array(say left array), keep moving ahead and keep product of all the elements to left of ith element.
2. In One array (say right array), keep product of elements to right of ith element. Do it in a single pass by calculating and placing the product from right to left.   
3. Multiply the element at ith location of left and right array and place them in the result array.   
## Approach 2: (Only constant extra Space)  (Space: O(1), Time: O(n))
1. Just Use the result array for all the calculations. No extra space
2. First Calculate all the left products in that array
3. In second pass keep calculating the right product and side by side multiply the right product with the value in result array(which is left product)
4. So, we multiply the left and right product.
## Approach 3: Everyhing in single pass. (Space: O(1), Time: O(n))
1. Similar to Approach 2
2. Just do both left asd right product at same time in same for loop.
3. ans[i] *= leftProd and ans[size-1-i] *= rightProd 
---

## Algorithm
---

## Edge Cases
---

## C++ Solution
```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> ans(nums.size());
        leftRightProdNoExtraSpace(nums, ans);
        return ans;    
    }

    void leftRightProdNoExtraSpace(const vector<int>& nums, vector<int>& ans){
        int curProd = 1;
        for(int i =0; i< nums.size(); ++i){
            ans[i] = curProd;
            curProd *= nums[i];  
        }

        curProd = 1;
        for(int i =nums.size()-1; i>=0 ; --i){
            ans[i] = ans[i]*curProd;
            curProd *= nums[i];  
        }
    }

    void leftRightProd(const vector<int>& nums, vector<int>& ans) {
        vector<int> leftProd(nums.size());
        vector<int> rightProd(nums.size());
        int curProd = 1;
        for(int i =0; i< nums.size(); ++i){
            leftProd[i] = curProd;
            curProd *= nums[i];  
        }

        curProd = 1;
        for(int i =nums.size()-1; i>=0 ; --i){
            rightProd[i] = curProd;
            curProd *= nums[i];  
        }

        for(int i =nums.size()-1; i>=0 ; --i){
            ans[i] = leftProd[i]*rightProd[i];
        }
    }
};
