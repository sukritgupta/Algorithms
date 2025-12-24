# Merge k Sorted Lists

**LeetCode:** (23) https://leetcode.com/problems/merge-k-sorted-lists/description/  
**Difficulty:** Hard  
**Pattern:** Min Heap  

---

## Problem Statement
"You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

 

Example 1:

Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted linked list:
1->1->2->3->4->4->5->6
Example 2:

Input: lists = []
Output: []
Example 3:

Input: lists = [[]]
Output: []
 

Constraints:

k == lists.length  
0 <= k <= 104  
0 <= lists[i].length <= 500  
-104 <= lists[i][j] <= 104  
lists[i] is sorted in ascending order.  
The sum of lists[i].length will not exceed 104."  

---

## Intuition


---

## Approach
- Push top k nodes in min heap, Take top(which is min), push next node.
- Side by side Keep adding node in new list"

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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
       return minHeap(lists);
        //return brute(lists);
    }
private:

    //Time Complexity: O(N log K)
    //Space Complexity: O(K)
    ListNode* minHeap(vector<ListNode*>& lists) {
        priority_queue<pair<int, ListNode*>, vector<pair<int, ListNode*>>, greater<>> pq;
        ListNode newHead;
        ListNode* curNode = &newHead;

        //Add k elemnts in pq
        for(int i=0; i<lists.size(); ++i){
            if(lists[i]){ pq.push({lists[i]->val, lists[i]});}
        }
        
        //while pq is not empty
        while(!pq.empty()){
            // take top insert, push top->next it it exists.
            curNode->next = pq.top().second; pq.pop();
            curNode = curNode->next;
            if(curNode->next) pq.push({curNode->next->val, curNode->next});
        }
        return newHead.next;
    }

    //Time Complexity(O(N*K))
    ListNode* brute(vector<ListNode*>& lists) {
        ListNode dummy;
        ListNode* newList = &dummy;
        int minListIndex =0;
        while(minListIndex != -1){
            int minVal = INT_MAX;
            minListIndex = -1; 
            for(int i=0; i<lists.size(); ++i){
                ListNode* curNode = lists[i];
                if(curNode && curNode->val<minVal){
                    minVal = curNode->val;
                    minListIndex = i;
                }
            }

            if(minListIndex != -1){
                newList->next = new ListNode(minVal);
                newList = newList->next;
                lists[minListIndex] = lists[minListIndex]->next;
            }
        }
        return dummy.next;
    }
};
