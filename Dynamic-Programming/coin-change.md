#Coin Chnage

**LeetCode:** (322) https://leetcode.com/problems/coin-change/description/
**Difficulty:** Medium  
**Pattern:** Dynamic Programming  

---

## Problem Statement
You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

 

Example 1:

Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
Example 2:

Input: coins = [2], amount = 3
Output: -1
Example 3:

Input: coins = [1], amount = 0
Output: 0
 

Constraints:

1 <= coins.length <= 12
1 <= coins[i] <= 231 - 1
0 <= amount <= 104  

---

## Intuition


---

## Approach (Recursion)
- Keep Subtracting coins recursilvely from amount and keep measuring min & current coins(height) & go till amount gets zero to find if it is a valid case.
- Base cond: when amount == 0, coins =0;

## Approach 2: Tabular
- `i th ` location in dp should indicate the minimum coins till that amount.
- Unbounded knapsack: for every amount, try taking each coin once more.
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
    unordered_map<int, int> dp;
public:
    int coinChange(vector<int>& coins, int amount) {
        if(amount <=0){return 0;}
        int count = coinChangeTab(coins, amount);
        return count==INT_MAX?-1:count;
    }

    int coinChangeRec(vector<int>& coins, int amount) {
        if(amount==0){
            return 0;
        }else if(amount<0){
            return INT_MAX;
        }
        if(dp.count(amount)) return dp[amount];
        int minDepth = INT_MAX;
        for(auto coin:coins){
            if(amount-coin>=0){
                int lowerDepth =  coinChangeRec(coins, amount-coin);
                if(lowerDepth<INT_MAX){
                    lowerDepth =  lowerDepth +1;
                    minDepth = min(minDepth, lowerDepth);
                } 
            }
        }
        dp[amount] = minDepth;
        return dp[amount];
    }

    int coinChangeTab(vector<int>& coins, int amount) {
        const int INF = amount +1;
        vector<int> dp1(amount+1, amount+1);
        dp1[0] = 0;
        for(int i=1; i<=amount; i++){
            for(auto coin:coins){
                if(i-coin>=0 ){
                    dp1[i] = min(dp1[i], 1+dp1[i-coin]);
                }
            }
        }
        return dp1[amount]==INF?-1:dp1[amount];
    }
};
