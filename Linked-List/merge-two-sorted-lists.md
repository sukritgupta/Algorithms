# Merge Two Sorted Lists

**LeetCode:** (21) https://leetcode.com/problems/merge-two-sorted-lists  
**Difficulty:** Easy  
**Pattern:** Linked List  

---

## Problem Statement
You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

 

Example 1:
<img width="662" height="302" alt="image" src="https://github.com/user-attachments/assets/d7ba9b4c-721a-4203-9ff2-55a18d6848bb" />


Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
Example 2:

Input: list1 = [], list2 = []
Output: []
Example 3:

Input: list1 = [], list2 = [0]
Output: [0]
 

Constraints:

The number of nodes in both lists is in the range [0, 50].
-100 <= Node.val <= 100
Both list1 and list2 are sorted in non-decreasing order.
---

## Intuition


---

## Approach1: Iterative
- In a new List merge nodes from both list, taking smaller 1 first. Add a dummy node first
## Approach 2: Recursive
Find the smaller node and call the recursion for remaining nodes. Add the result to current list.
- Here swap is done to use just one variable for the node which is smaller.
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
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        return Rec(list1, list2);
    }

    ListNode* itr(ListNode* list1, ListNode* list2) {
        ListNode* newHead;
        ListNode* newList = new ListNode(); //dummy
        newHead = newList;
        while(list1 && list2){
            if(list1->val > list2->val){
                newList->next = list2;
                //ListNode *list2Next = list2->next;
                list2 = list2->next;
            }else{
                newList->next = list1;
                //ListNode *list2Next = list2->next;
                list1 = list1->next;
            }
            newList = newList->next;
        }
        
        newList->next = list1?list1:list2;
        ListNode *head = newHead->next;
        delete newHead; 
        return head;
    }

    ListNode* Rec(ListNode* list1, ListNode* list2) {
        if(!list1 || !list2){
            return list1?list1:list2;
        }
        if(list1->val > list2->val){
            swap(list1, list2);
        }

        list1->next = Rec(list1->next, list2); //list = curNode + received List
        return list1;
    }
};
