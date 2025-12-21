# Valid Parentheses

**LeetCode:** (20) https://leetcode.com/problems/valid-parentheses  
**Difficulty:** Easy  
**Pattern:** Stack,   

---

## Problem Statement
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.
 

Example 1:

Input: s = "()"

Output: true

Example 2:

Input: s = "()[]{}"

Output: true

Example 3:

Input: s = "(]"

Output: false

Example 4:

Input: s = "([])"

Output: true

Example 5:

Input: s = "([)]"

Output: false

 

Constraints:

1 <= s.length <= 104
s consists of parentheses only '()[]{}'.
---

## Intuition


---

## Approach
push on Open bracket, match top on closing bracket

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
    bool isValid(string s) {
        stack<char> pStack;
        const unordered_map<char, char> pMap = {{'}', '{'},{')', '('} , {']', '['}};
        for (char c : s) {
            if (pMap.find(c)==pMap.end()) {
                pStack.push(c);
            } else if (!pStack.empty() && pStack.top()==pMap.at(c)) {
                pStack.pop();
            } else {
                return false;
            }
        }
        return pStack.empty();
    }
};
