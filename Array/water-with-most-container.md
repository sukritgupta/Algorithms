# Water With Most Container

**LeetCode:** (11) https://leetcode.com/problems/container-with-most-water/description/  
**Difficulty:** Medium  
**Pattern:** Array, Two Pointer

---

## Problem Statement
You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

 

Example 1:  
<img width="801" height="383" alt="image" src="https://github.com/user-attachments/assets/28d7ccdf-668b-4705-a7e1-6293985e6355" />


Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
Example 2:

Input: height = [1,1]
Output: 1
 

Constraints:

n == height.length
2 <= n <= 105
0 <= height[i] <= 104
---

## Intuition


---

## Approach
Maximize area. Take Two Pointers at both end. Move the smaller pointer inwards and keep track of max area.
---

## Key Insights
- area = min(height[j], height[i]) * (j-i)
- Moving the smaller pointer is definitely correct as:
  - The max contribution of that pointer is already done as
  - when we are going to move left x axis distance is going to decrease and
  - its height is going to remain same, so we are never going to get a better solution.
- Also mathematically, if we want to increase area:
- j-i(distance along x) is always going to decrease, so we need to increase the other part.
- min(height[j], height[i]) will increase when we'll increase the minimum part.  
---

## Mistakes
---

## Edge Cases
---

## C++ Solution
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int i=0, j=height.size()-1, maxWater = 0;
        while(i<j){
            int waterContained = (j-i)* min(height[i], height[j]);
            maxWater = max(maxWater, waterContained);
            if(height[i]<height[j]){
                ++i;
            }else{
                --j;
            }
        }
        return maxWater;
    }
};
