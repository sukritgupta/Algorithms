# Invert Binary Tree

**LeetCode:** (226) https://leetcode.com/problems/invert-binary-tree  
**Difficulty:** Easy  
**Pattern:** Tree  

---

## Problem Statement
Given the root of a binary tree, invert the tree, and return its root.

 

Example 1:
<img width="911" height="301" alt="image" src="https://github.com/user-attachments/assets/6c7cd414-f899-42ab-833d-f5b83bdee6f9" />


Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]
Example 2:

<img width="761" height="182" alt="image" src="https://github.com/user-attachments/assets/24c00936-3eb4-47b7-ad65-0de135287616" />

Input: root = [2,1,3]
Output: [2,3,1]
Example 3:

Input: root = []
Output: []
 

Constraints:

The number of nodes in the tree is in the range [0, 100].
-100 <= Node.val <= 100

---

## Intuition


---

## Approach
- Swap left and right nodes  
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
    TreeNode* invertTree(TreeNode* root) {
        if(!root) return root;
        return swapNodeRec(root);
        //swapNodeItr(root);
        //return root;
    }

    TreeNode* swapNodeRec(TreeNode* root) {
        if(!root) return root;
        swap(root->left, root->right); 
        swapNodeRec(root->left);
        swapNodeRec(root->right);
        return root;
    }

    void swapNodeItr(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            TreeNode* curNode = q.front(); q.pop();
            swap(curNode->left, curNode->right);
            if(curNode->left) q.push(curNode->left);
            if(curNode->right) q.push(curNode->right);    
        }
    }
};
