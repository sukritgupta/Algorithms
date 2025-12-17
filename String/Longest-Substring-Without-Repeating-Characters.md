# Longest Substring Without Repeating Characters

**LeetCode:** (3) https://leetcode.com/problems/best-time-to-buy-and-sell-stock  
**Difficulty:** Medium  
**Pattern:** String, Sliding Window, Hashing, Two Pointer  

---

## Problem Statement
"Given a string s, find the length of the longest substring without duplicate characters.

 

Example 1:

Input: s = ""abcabcbb""
Output: 3
Explanation: The answer is ""abc"", with the length of 3. Note that ""bca"" and ""cab"" are also correct answers.
Example 2:

Input: s = ""bbbbb""
Output: 1
Explanation: The answer is ""b"", with the length of 1.
Example 3:

Input: s = ""pwwkew""
Output: 3
Explanation: The answer is ""wke"", with the length of 3.
Notice that the answer must be a substring, ""pwke"" is a subsequence and not a substring.
 

Constraints:

0 <= s.length <= 5 * 104
s consists of English letters, digits, symbols and spaces."
---

## Intuition

---

## Approach
- Take left, right pointer, Keep putitng chars with index in map, if already there and its index >=left, update index and move left to index +1  
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
    int lengthOfLongestSubstring(string s) {
        map<char, int> charMap;
        int left = 0;
        int maximum =0;
        for (int right = 0; right < s.size(); ++right) {
            const auto& itr = charMap.find(s[right]);
            if (itr != charMap.end() && itr->second >= left) {
                left = itr->second + 1;
            } else {
                maximum = max(maximum, right - left + 1);
            }
            charMap[s[right]] = right;
        }
        return maximum;
    }
};
