# Maximum Depth of Binary tree

**LeetCode:** (104) https://leetcode.com/problems/maximum-depth-of-binary-tree 
**Difficulty:** Easy  
**Pattern:** Tree

---

## Problem Statement
Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

 

Example 1:
<img width="422" height="292" alt="image" src="https://github.com/user-attachments/assets/3978f2e2-f4f9-4a1e-9206-036559390dab" />


Input: root = [3,9,20,null,null,15,7]
Output: 3
Example 2:

Input: root = [1,null,2]
Output: 2
 

Constraints:

The number of nodes in the tree is in the range [0, 104].
-100 <= Node.val <= 100
---

## Intuition


---

## Approach 1(Recursive)
- Take max of height of left and right and +1
## Approach 2: Iterative
Number of levels in BFS (count how many times the queue is emptied level-wise).”
- Queue contains exactly one level at a time.
- depth++, Push all elements together and remove them together.
---

## Key Insights
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
    int maxDepth(TreeNode* root) {
        return maxDepthRec(root);
        //return maxDepthItr(root);
    }

    int maxDepthRec(TreeNode* root) {
        if(!root) return 0;
        return 1+ max(maxDepthRec(root->left), maxDepthRec(root->right));  
    }

    int maxDepthItr(TreeNode* root) {
        if(!root) return 0;
        queue<TreeNode*> q;
        q.push(root);
        int depth =0;

        while(!q.empty()){
            depth++;
            int qSize = q.size();

            while(qSize--){
                TreeNode* node = q.front(); q.pop();
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
            }
        }
        return depth;     
    }
};
