# Validate Binary Search Tree

**LeetCode:** (98) https://leetcode.com/problems/validate-binary-search-tree
**Difficulty:** Medium  
**Pattern:** Tree, DFS  

---

## Problem Statement
Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

The left subtree of a node contains only nodes with keys strictly less than the node's key.
The right subtree of a node contains only nodes with keys strictly greater than the node's key.
Both the left and right subtrees must also be binary search trees.
 

Example 1:
<img width="302" height="182" alt="image" src="https://github.com/user-attachments/assets/c219941e-e5cb-4097-ab7a-1555ba25ea54" />


Input: root = [2,1,3]
Output: true
Example 2:
<img width="422" height="292" alt="image" src="https://github.com/user-attachments/assets/4c25adf5-ce14-4735-8a2e-07d66daef2bd" />


Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
 

Constraints:

The number of nodes in the tree is in the range [1, 104].
-231 <= Node.val <= 231 - 1
---

## Intuition


---

## Approach
1. **Validate BST using global `(min, max)` bounds, not parent comparison.**
2. **Use strict `<` and `>` checks — duplicates are invalid.**
3. **Bounds must be `long long` to safely handle `INT_MIN / INT_MAX`.**

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
    bool isValidBST(TreeNode* root) {
        return isValidBSTRec(root, LLONG_MIN, LLONG_MAX); 
    }

    bool isValidBSTRec(TreeNode* root, long long min, long long max){
        if(!root) return true;
        if(root->val<= min || root->val>=max) return false;
        return isValidBSTRec(root->left, min, root->val) 
                && isValidBSTRec(root->right, root->val, max);
    }
};
