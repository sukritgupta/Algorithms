# Binary Tree Level Order Traversal

**LeetCode:** (102) https://leetcode.com/problems/best-time-to-buy-and-sell-stock  
**Difficulty:** Medium  
**Pattern:** Tree, Level Order  

---

## Problem Statement
---

## Intuition


---

## Approach
Level Order = BFS → queue → process q.size() nodes per level.
---

## Key Insights
To improve performance, set vector size by callling `vec.reserve(sz)`.
---

## Mistakes
---

## Edge Cases
---

## C++ Solution
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if (!root) return result;

        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            int sz = q.size();
            vector<int> level;
            level.reserve(sz);

            for (int i = 0; i < sz; ++i) {
                TreeNode* node = q.front(); q.pop();
                level.push_back(node->val);
                if (node->left)  q.push(node->left);
                if (node->right) q.push(node->right);
            }

            result.push_back(level);
        }
        return result;
    }
};
