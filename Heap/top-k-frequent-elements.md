# Top K Frequent Elements

**LeetCode:** (347) https://leetcode.com/problems/top-k-frequent-elements  
**Difficulty:** Medium  
**Pattern:** Heap, Vector,  Min Heap  

---

## Problem Statement
"Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

 

Example 1:  
Input: nums = [1,1,1,2,2,3], k = 2  
Output: [1,2]  

Example 2:   
Input: nums = [1], k = 1  
Output: [1]  

Example 3:  
Input: nums = [1,2,1,2,1,2,3,1,3,2], k = 2  
Output: [1,2]  

Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104
k is in the range [1, the number of unique elements in the array].
It is guaranteed that the answer is unique.

Follow up: Your algorithm's time complexity must be better than O(n log n), where n is the array's size."

---

## Intuition


---

## Approach  
**Buckets(O(n)):** Count Frequency in Map -> Take n+1 vec of vec. With Frequency as key push the nums in arrays. There can be multiple nums with same freq.  
**MinHeap O(nlogk):** Count Freq in Map -> Put max k elemets in heap and pop if more than k. min heap will finally contain k top elements     
**MaxHeap O(nlogn):** Count freq in map. Put all in MaxHeap, take top k elems  

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
    vector<int> topKFrequent(vector<int>& nums, int k) {
        // maxHeap   → simple but slower (O(n log n))
        // minHeap   → optimal for small k (O(n log k))
        // buckets   → best asymptotic time (O(n))

        //return maxHeap(nums, k);
        //return minHeap(nums, k);
        return buckets(nums, k);
    }

private:

    // ===================== BUCKET SORT (HASH MAP + VECTOR) =====================
    // Hook:
    // Frequency of any element is at most n.
    // We bucket elements by frequency and scan from highest to lowest.
    // Avoids heap entirely → linear time.

    // Time:  O(n)
    // Space: O(n)
    vector<int> buckets(vector<int>& nums, int k) {

        vector<int> result;

        // Step 1: Count frequency of each number
        unordered_map<int, int> counter;
        counter.reserve(nums.size());  // optimization: reduce rehashing
        for (auto num : nums) {
            counter[num]++;
        }

        // Step 2: Create buckets where index = frequency
        // Size = nums.size() + 1 because max frequency can be n
        vector<vector<int>> buckets(nums.size() + 1);

        // Place numbers into their corresponding frequency bucket
        for (auto [num, freq] : counter) {
            buckets[freq].push_back(num);
        }

        // Step 3: Traverse buckets from highest frequency to lowest
        for (int i = nums.size(); i >= 0 && k > 0; --i) {
            for (auto num : buckets[i]) {
                result.push_back(num);
                --k;
                if (k == 0) break;
            }
        }

        return result;
    }

    // ===================== MIN HEAP (HASH MAP + HEAP OF SIZE K) =====================
    // Hook:
    // Keep only the best k frequent elements in a min-heap.
    // Heap size is capped at k → heap operations cost log(k), not log(n).
    // Most practical and interview-preferred solution.

    // Time:  O(n log k)
    // Space: O(k)
    vector<int> minHeap(vector<int>& nums, int k) {

        vector<int> result;

        // Step 1: Frequency count
        unordered_map<int, int> counter;
        for (auto num : nums) {
            counter[num]++;
        }

        // Min-heap storing {frequency, number}
        priority_queue<
            pair<int, int>,
            vector<pair<int,int>>,
            greater<>
        > q;

        // Step 2: Maintain heap size <= k
        for (auto [num, freq] : counter) {
            q.push({freq, num});
            if (q.size() > k) {
                q.pop();  // remove least frequent element
            }
        }

        // Step 3: Extract result
        while (!q.empty()) {
            result.push_back(q.top().second);
            q.pop();
        }

        return result;
    }

    // ===================== MAX HEAP (HASH MAP + FULL HEAP) =====================
    // Hook:
    // Push all elements into a max-heap and extract top k.
    // Simple and intuitive, but heap grows to size n.
    // Slower due to log(n) heap operations.

    // Time:  O(n log n)
    // Space: O(n)
    vector<int> maxHeap(vector<int>& nums, int k) {

        vector<int> result;

        // Step 1: Frequency count
        unordered_map<int, int> counter;
        for (auto num : nums) {
            counter[num]++;
        }

        // Max-heap storing {frequency, number}
        priority_queue<pair<int, int>> q;
        for (auto [num, freq] : counter) {
            q.push({freq, num});
        }

        // Step 2: Extract top k elements
        for (int i = 0; i < k; ++i) {
            result.push_back(q.top().second);
            q.pop();
        }

        return result;
    }
};
