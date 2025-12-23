# Number of 1 Bits

**LeetCode:** (191) https://leetcode.com/problems/number-of-1-bits  
**Difficulty:** Easy  
**Pattern:** Bit Manip, Brain Kernighen  

---

## Problem Statement
"Given a positive integer n, write a function that returns the number of set bits in its binary representation (also known as the Hamming weight).

 

Example 1:

Input: n = 11

Output: 3

Explanation:

The input binary string 1011 has a total of three set bits.

Example 2:

Input: n = 128

Output: 1

Explanation:

The input binary string 10000000 has a total of one set bit.

Example 3:

Input: n = 2147483645

Output: 30

Explanation:

The input binary string 1111111111111111111111111111101 has a total of thirty set bits.

 

Constraints:

1 <= n <= 231 - 1
 

Follow up: If this function is called many times, how would you optimize it?"  

---

## Intuition


---

## Approach
"Brain Kernighen=> n=n&(n-1) drops the last 1, count while dropping (O(no of 1s in num))
Apr2 : Check last bit n&1 cnt ++, n >>=1 (shift right) O(32) constant"

---

## Key Insights
---

## Mistakes
---

## Edge Cases
---

## C++ Solution
```cpp
