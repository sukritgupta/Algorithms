# Best Time to Buy and Sell Stock

**LeetCode:** (121) https://leetcode.com/problems/best-time-to-buy-and-sell-stock  
**Difficulty:** Easy  
**Pattern:** Array  

---

## Problem Statement
You are given an array prices where prices[i] is the price of a given stock on the ith day.  
You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.  
Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.  

Example 1:  
Input: prices = [7,1,5,3,6,4]  
Output: 5  
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.  
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.  
Example 2:  
Input: prices = [7,6,4,3,1]  
Output: 0  
Explanation: In this case, no transactions are done and the max profit = 0.  

Constraints:  
 1 <= prices.length <= 105
 0 <= prices[i] <= 104
 
---

## Intuition
Best Sale price will always be the max number from end.

---

## Approach
1. Find the best day possible in future
	a. Traverse from right to left and find the max till that and fill a new vector with the max possible rate after that date
	b. In another pass traverse both the vec and subtract the actual price and max price and keep the max possible.
## Approach 2: (Only constant extra Space)  
1. Rather than keeping a separate vector, keep a variable which keeps the current max sale price.  
2. Iterate from right to left and maintain max profit and max sale price.  
---

## Algorithm
1. For each element:
   - If `(target - current)` exists in the map, return both indices.
   - Otherwise, store the current element with its index.

---

## Complexity
- **Time:** `O(n)`
- **Space:** `O(n)`

---

## Edge Cases
---

## C++ Solution
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        
        return bestSaleDayOneSpace(prices);
    }

    int bestSaleDayOneSpace(vector<int>& prices){
        int maxP = 0;
        int curMaxSell = 0;
        int days = prices.size();
        for(int i= days-1; i>=0; --i){
            maxP  = max(maxP, curMaxSell - prices[i]);
            curMaxSell = max(curMaxSell, prices[i]);
        }
        return maxP;
    }

    int bestSaleDay(vector<int>& prices){
        int maxP = 0;
        int days = prices.size();
        vector<int> maxPossPrice(days);
        
        int curMax = prices[days-1];
        for(int i= days-1; i>=0; --i){
            curMax = max(curMax, prices[i]);
            maxPossPrice[i] = curMax;
        }

        for(size_t i=0; i<days; ++i){
            maxP = max(maxP, maxPossPrice[i]-prices[i]);
        }
        return maxP;
    }

    int bruteForce(vector<int>& prices){
        int maxP = 0;
        for(size_t i=0; i<prices.size(); ++i){
            for(size_t j=i+1; j<prices.size();++j){
                if(prices[j]-prices[i]>maxP){
                    maxP = prices[j]-prices[i];
                }
            }
        }
        return maxP;
    }
};
