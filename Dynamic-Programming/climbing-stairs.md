#Climbing Stairs

**LeetCode:** (70) https://leetcode.com/problems/climbing-stairs 
**Difficulty:** Easy  
**Pattern:** Dynamic Programming, fibonacci  

---

## Problem Statement
You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

 

Example 1:

Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
Example 2:

Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
 

Constraints:

1 <= n <= 45
---

## Intuition


---

## Approach 
To get to any `nth` stair, we can either get from n-1 or n-2 stairs, so total ways of reachig there are no_of_ways_to_reach(n-1) +  no_of_ways_to_reach(n-2).
It becomes similar to fibonacci series.
Once recursion is established, convert to memoization, tabularization, optimization
## Approach 2: ()  
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
    vector<int> dp =  vector<int>(46, -1);

public:
    int climbStairs(int n) {
        //return climbStairsRec(n);
        //return climbStairsMemo(n);
        //return climbStairsTabu(n);
        return climbStairsOpt(n);
    }

    int climbStairsRec(int n) {
        if(n==0 || n==1) return 1;
        return climbStairsRec(n-1)+ climbStairsRec(n-2);
    }
    
    int climbStairsMemo(int n) {
        if(n==0 || n==1) return 1;
        if(dp[n] !=-1) return dp[n];
        dp[n] = climbStairsMemo(n-1)+ climbStairsMemo(n-2);
        return dp[n];
    }

    int climbStairsTabu(int n) {
        dp[0] = 1;
        dp[1] = 1;
        for(int i=2; i<=n; ++i){ 
            dp[i] = dp[i-1]+ dp[i-2];
        }
        return dp[n];
    }

    int climbStairsOpt(int n) {
        int prev1 = 1;
        int prev2 = 1;
        for(int i=2; i<=n; ++i){ 
            int cur = prev1 + prev2;
            prev2 = prev1;
            prev1 = cur;
        }
        return prev1;
    }

};
