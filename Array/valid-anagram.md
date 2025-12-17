# Valid Anagram

**LeetCode:** (242) https://leetcode.com/problems/valid-anagram  
**Difficulty:** Easy  
**Pattern:** String, Hashing  

---

## Problem Statement
Given two strings s and t, return true if t is an anagram of s, and false otherwise.

 

Example 1:

Input: s = "anagram", t = "nagaram"

Output: true

Example 2:

Input: s = "rat", t = "car"

Output: false

 

Constraints:

1 <= s.length, t.length <= 5 * 104
s and t consist of lowercase English letters.
 

Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?
---

## Intuition

---

## Approach
- Keep count of the occured chars in first string in Hash and reduce them while counting for second.
---

## Key Insights
- Array can be initialized with zeros by arr[5] = {}
---

## Mistakes
---

## Edge Cases
---

## C++ Solution
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        return array(s,t);
        //return hashMap(s,t);
    }

    bool hashMap(string s, string t) {
        if(s.size()!=t.size()){
            return false;
        }
        unordered_map<char, int> counter;
        for(char c: s){
            ++counter[c];
        }
        for(char c: t){
            if(counter.find(c) == counter.end() || counter[c] == 0){
                return false;
            }
            --counter[c];
        } 
        return true;
    }

    bool array(string s, string t) {
        if(s.size()!=t.size()){
            return false;
        }

        constexpr int nc = 26;
        int sa[nc] = {};// initializes to zero

        for(int i=0; i<s.size(); ++i ){
            ++sa[s[i]-'a'];
            --sa[t[i]-'a'];
        }

        for(int i=0; i<nc; ++i ){
            if(sa[i] !=0){
                return false;
            }
        }
        return true;
    }
};
