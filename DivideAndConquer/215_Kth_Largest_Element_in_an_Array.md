# 215. Kth Largest Element in an Array

2020/06/23 ZTH

### Problem Description

Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

**Example 1:**

```
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```



### Algorithm

Way1: Sorting

* Sort the whole list in descending order and return the k-th element in the sorted list
* Complexity Analysis:
  * Time: O(nlogn)
  * Space: O(1) no extra space, not considering input list

Way2: Heap

* Keep a heap with size k storing k largest elements
* Complexity Analysis:
  * Time: O(nlogt)
  * Space: O(t)



### Code

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # sort function: O(nlogn) time, O(1) space
        nums.sort(reverse=True)
        return nums[k-1]
```

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # heap: O(nlogt) time, O(t) space
        return heapq.nlargest(k, nums)[-1]
```

