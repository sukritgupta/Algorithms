# Number of Islands

**LeetCode:** (200) https://leetcode.com/problems/number-of-islands  
**Difficulty:** Medium  
**Pattern:** Graph, BFS, DFS  

---

## Problem Statement
Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

 

Example 1:

Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
Example 2:

Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
 

Constraints:

m == grid.length
n == grid[i].length
1 <= m, n <= 300
grid[i][j] is '0' or '1'.
---

## Intuition


---

## Approach BFS
Keep Visited array,
“Scan grid → on every unvisited ‘1’, flood-fill (BFS/DFS) → count++.”
“Mark visited when pushing, not when popping.”
---

## Key Insights
“Mark visited when pushing, not when popping.”
---

## Mistakes
---

## Edge Cases
---

## C++ Solution
```cpp
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int m = grid.size();
        int n=  grid[0].size();
        vector<vector<int>> visited(m, vector<int>(n,0));
        //visited.fill(0);
        int numIsland = 0;
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                if(grid[i][j] =='1' && !visited[i][j]){
                    bfs(grid, m,n, visited, i,j);
                    ++numIsland;
                }
            }
        } 
        return  numIsland;
    }
private:
    void bfs(vector<vector<char>>& grid, int m, int n, vector<vector<int>>& visited, int i, int j){
        queue<pair<int, int>> q;
        q.push({i,j});
        visited[i][j] = 1;
        int directions[][2] = {{-1,0}, {0,-1}, {0,1}, {1,0}};
        while(!q.empty()){
            auto [k, l] = q.front(); q.pop();
             
             for(auto [rDir, cDir]: directions){
                int nRow = k+rDir;
                int nCol = l+cDir;

                if(nRow>=0 && nRow< m && nCol >=0 && nCol <n 
                    && grid[nRow][nCol] == '1' && !visited[nRow][nCol]){
                    q.push({nRow,nCol});
                    visited[nRow][nCol] = 1;
                }
             }
        }
    }
};
