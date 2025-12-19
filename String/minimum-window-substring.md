# Minimum Window Substring

**LeetCode:** (76) https://leetcode.com/problems/minimum-window-substring/description/  
**Difficulty:** Hard  
**Pattern:** String, Sliding Window  
**Stats:** Unable to solve in multiple attemps, Found difficult, Rep needed
---

## Problem Statement
Given two strings s and t of lengths m and n respectively, return the minimum window substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

 

Example 1:

Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
Example 2:

Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
Example 3:

Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
 

Constraints:

m == s.length
n == t.length
1 <= m, n <= 105
s and t consist of uppercase and lowercase English letters.
 

Follow up: Could you find an algorithm that runs in O(m + n) time?
---

## Intuition


---

## Approach
Find the window in which all t chars exist and then shrink window, if required char goes out expand window
- Update count of all `t chars` in array:: arr[128].
- Keep count of chars to be found :: `reqNumChars` 
- Take left and right and move right till all the `t chars` are found.
- keep decrementing `reqNumChars`, if arr[s[right]] >0 
- the decrement arr[s[right]] 
  - **[!imp]** Note in arr, count of non `t chars` can be atmost 0 at any time, since we always  decrement before incrementing
  - For `t chars`, we may also go in negative (s= "bba", t="ba"), so we only want to decrement `reqNumChars` if it is >0
- Once we find a window we try to shrink window from left and keep the minima
  - It is non `t char`, keep on incrementing left, If it is `t char` also increment the `reqNumChars`.
  - Again, we only increase `reqNumChars`, if arr[s[right]]>0 after doing  s[right]++; 
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
    string minWindow(string s, string t) {
        return minWindowArr(s,t);
    }    
    string minWindowArr(string s, string t) {
        if(s=="" || t=="" ||s.size()<t.size()){
            return "";
        }
        int requiredChars = t.size();
        int left = 0, right =0;
        int minStart=-1;
        int minLen = INT_MAX;
        int arr[128]={0};
        for(char c: t){arr[c]++;}
        for(int right=0; right<s.size(); ++right){
            char rightChar = s[right];
            if(arr[rightChar]>0){
                --requiredChars;
            }
            arr[rightChar]--;
            
            while(requiredChars==0){
                if(right - left + 1 < minLen){  // Check if strictly smaller
                    minLen = right - left + 1;
                    minStart = left;
                }
                arr[s[left]]++;
                if(arr[s[left]]>0){
                    requiredChars++;
                }
                left++;
            }
        }
        return minStart == -1?"":s.substr(minStart, minLen);
    }

    string minWindowMap(string s, string t) {
        if(s=="" || t=="" ||s.size()<t.size()){
            return "";
        }
        int requiredChars = t.size();
        int left = 0, right =0;
        int minStart=-1;
        int minLen = INT_MAX;
        //int arr[128]={0};
        unordered_map<char, int> arr;
        for(char c: t){arr[c]++;}
        for(int right=0; right<s.size(); ++right){
            char rightChar = s[right];
            if(arr.find(rightChar)!=arr.end()){
                --arr[rightChar];
                if(arr[rightChar] >=0){
                    --requiredChars;
                }   
            }
            while(requiredChars==0){
                
                if(right - left + 1 < minLen){  // Check if strictly smaller
                    minLen = right - left + 1;
                    minStart = left;
                }
                if(arr.find(s[left])!=arr.end()){
                    arr[s[left]]++;
                    if(arr[s[left]]>0)
                    {
                        requiredChars++;
                    }
                }
                left++;
            }
        }
        return minStart == -1?"":s.substr(minStart, minLen);
    }
};
