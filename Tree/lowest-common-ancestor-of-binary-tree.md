# Lowest Common Ancestor of a Binary Tree

**LeetCode:** (236)   
**Difficulty:** Medium  
**Pattern:** Tree  

---

## Problem Statement
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

 

Example 1:
<img width="200" height="190" alt="image" src="https://github.com/user-attachments/assets/219667c7-1812-48e0-a9c2-b0b0046dc2ad" />


Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
Example 2:
<img width="200" height="190" alt="image" src="https://github.com/user-attachments/assets/113b8aee-ab03-4ffa-8b9a-9ab37a075f55" />


Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
Example 3:

Input: root = [1,2], p = 1, q = 2
Output: 1
 

Constraints:

The number of nodes in the tree is in the range [2, 105].
-109 <= Node.val <= 109
All Node.val are unique.
p != q
p and q will exist in the tree.

---

## Intuition


---

## Approach
- Solution relies on fact that solution is must present.
- Consider where the expected nodes can be present: in same left branch, in same right branch or one in left, one in right.
- Make cases as per  this logic.
- If we find one element in a branch, return from there without looking for other one. look for other one in other side branch.
- If found return root else return the found left or right branch.
  
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
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
       
       return lowestCommonAncestorMin(root, p, q);
       /* vector<TreeNode*> pPath; 
        vector<TreeNode*> qPath; 
        findPath(root, p, pPath);
        findPath(root, q, qPath);

        for(auto node: qPath){
            cout<< "qPath "<<node->val<<endl;
            if(count(pPath.begin(), pPath.end(), node)){
                return node;
            }
        }
        return nullptr;*/

    }

    TreeNode* lowestCommonAncestorMin(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root || root == p || root == q){
            return root;
        }

        TreeNode* left = lowestCommonAncestorMin(root->left, p, q);
        TreeNode* right = lowestCommonAncestorMin(root->right, p, q);

        if(left && right){
            return root;
        }

        return left?left:right;
    }

    bool findPath(TreeNode* root, TreeNode* node, vector<TreeNode*>& pPath){
        if(!root) return false;
        if(root == node){
            pPath.push_back(root);
            return true;
        } 

        int found = false;
        if(!found) found = findPath(root->left, node, pPath);
        if(!found) found = findPath(root->right, node, pPath);
        if(found ){
            pPath.push_back(root);
        }
        return found;
    }
};
