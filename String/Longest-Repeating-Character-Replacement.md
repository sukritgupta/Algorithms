#Longest Repeating Character Replacement

**LeetCode:** (424) https://leetcode.com/problems/longest-repeating-character-replacement  
**Difficulty:** Medium  
**Pattern:** String, Sliding window, Two pointer, Hash  

---

## Problem Statement
"You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.
 
Example 1:

Input: s = ""ABAB"", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.
Example 2:

Input: s = ""AABABBA"", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form ""AABBBBA"".
The substring ""BBBB"" has the longest repeating letters, which is 4.
There may exists other ways to achieve this answer too.
 

Constraints:

1 <= s.length <= 105
s consists of only uppercase English letters.
0 <= k <= s.length"
---

## Intuition


---

## Approach  
We need to maximize the most repeating character in the current window.
We are only concerned about count of most repeating character in the window, whatever character it may be.
- Keep a HashMap of character which keeps counter of charcters in current window.
  - When an element leaves window decrement its count, when an element enters window increment its count.
  - Add the elements to the window till `right-left+1 - maxFreq <=k`
  - if window cannot grow increment left and decrease that element count from map.
---

## Key Insights
- We only need to consider maximum maxFreq, we don't need to lower it or recalculate it if window changes.
- Because to get even more maxCount, we need bigger window, window can only get big if maxFreq is more as max window size = maxFreq + k
- k is constant, to increase max window size we need to increase maxFreq. 

## Mistakes
---

## Edge Cases
---

## C++ Solution
```cpp
class Solution {
public:
    int characterReplacement(string s, int k) {
        int left=0, right=0, maxFreq=0, maxCount=0;
        //keeps count of characters in current window
        unordered_map<char,int> counter;

        while(right<s.size()){
            counter[s[right]]++;
            //maxFreq keeps the max count of any repeating character at any time we had in any window,
            //regardless of what is window now
            maxFreq = max(maxFreq, counter[s[right]]);   
            if(right-left+1 - maxFreq <= k){
                maxCount = max(maxCount, right-left+1);
            }else{
                counter[s[left]]--;
                left++;
            }
            right++;
        }
        return maxCount;
    }
};
