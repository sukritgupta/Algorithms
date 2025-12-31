# Word Search

**LeetCode:** (79) https://leetcode.com/problems/word-search/description  
**Difficulty:** Medium  
**Pattern:** BackTracking DFS  

---

## Problem Statement
Given an m x n grid of characters board and a string word, return true if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

 

Example 1:
<img width="322" height="242" alt="image" src="https://github.com/user-attachments/assets/26aca8d2-f90e-45d0-a227-44342d4ca8ec" />


Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
Example 2:

<img width="322" height="242" alt="image" src="https://github.com/user-attachments/assets/f7029132-9106-41f1-855d-3b549d27661e" />

Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
Example 3:
<img width="322" height="242" alt="image" src="https://github.com/user-attachments/assets/9d00a4b0-d38a-4270-82f0-5cbba1d48a2b" />


Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
 

Constraints:

m == board.length
n = board[i].length
1 <= m, n <= 6
1 <= word.length <= 15
board and word consists of only lowercase and uppercase English letters.
 

Follow up: Could you use search pruning to make your solution faster with a larger board?

 

---

## Intuition


---

## Approach (T: O(n*m*4^L))
- DFS: Check the cur char and if its correct go top/down/left/right.
- Check above for all n*m 
        //Prune1: board should be >= word size
        //Prune 2: Use less repeating char at start  (great boost as unique elems in start lead to better decision and less branching)
        //Prune 3: All the word Characters should be present on board(great boost as n*m is much better than going exponential

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
    bool exist(vector<vector<char>>& board, string word) {
        int m = board.size();
        int n = board[0].size();

        //Prune1: board should be >= word size
        if(m*n<word.size()){return false;}

        //Prune 2: Use less repeating char at start  
        unordered_map<char, int> count;
        for(char c : word) {
            count[c]++;
        }
        if(count[word[0]] > count[word.back()]) {
            reverse(word.begin(), word.end());
        }

        //Prune 3: All the word Characters should be present on board
        unordered_map<char, int> boardCount;
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                boardCount[board[i][j]]++;
            }
        }        
        for(char c : word) {
            if(--boardCount[c]<0) return false;
        }

        vector<vector<bool>> visited(m, vector<bool>(n,0));
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                bool res = existsRec(board,  word, visited, 0,  i, j,m,n);
                if(res) return true;
            }
        }
        return false;
    }

    bool existsRec(vector<vector<char>>& board, string& word, vector<vector<bool>>& visited, 
                        int ch, int i, int j, int m, int n){
        if(ch == word.size())
           return true;
        if( i<0 || i>=m || j <0 || j>=n || visited[i][j] || word[ch] != board[i][j]){
            return false;
        }
        visited[i][j] = true;
        int dirs[4][2] = {{-1,0},{0, -1}, {1,0}, {0,1}};
        for(auto&[k,l]: dirs){
            int newi = i+k;
            int newj = j+l; 
            bool found = existsRec(board,  word, visited, ch+1, newi,  newj, m, n);
            if(found) {
                visited[i][j] =false;
                return found;
            }
        }
        visited[i][j] =false;
        return false;
    }
};
