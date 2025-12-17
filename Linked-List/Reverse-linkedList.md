# Reverse Linked List

**LeetCode:** (206) https://leetcode.com/problems/reverse-linked-list  
**Difficulty:** Easy  
**Pattern:** Linked List  

---

## Problem Statement
Given the head of a singly linked list, reverse the list, and return the reversed list.

 

Example 1:


Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
Example 2:


Input: head = [1,2]
Output: [2,1]
Example 3:

Input: head = []
Output: []
 

Constraints:

The number of nodes in the list is the range [0, 5000].
-5000 <= Node.val <= 5000

Follow up: A linked list can be reversed either iteratively or recursively. Could you implement both?

---

## Intuition


---

## Approach
- "Make the previous node, next of current node.
- For recursive, iterate till end and get new node, head->next->next=head;"
---

## Algorithm
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
    ListNode* reverseList(ListNode* head) {
        return rec(head);
        //return itr(head);
    }

    ListNode* rec(ListNode *head){
        if(!head || !head->next){
            return head;
        }
        ListNode* newHead = rec1(head->next); 
        head->next->next = head;
        head->next= nullptr;
        return newHead;    
    }

    //simpler approach could be prevNode = nullptr and currNode = head
    ListNode* itr(ListNode *head){
        ListNode* prevNode = nullptr, *curNode = head, *nextNode = nullptr;
        while(curNode != nullptr){
            nextNode = curNode->next;
            curNode->next = prevNode;
            prevNode = curNode;
            curNode = nextNode;
        }
        return prevNode; 
    }
};
