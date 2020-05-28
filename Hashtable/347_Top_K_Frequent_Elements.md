# 347. Top K Frequent Elements

2020/05/28 ZTH

### Problem Description

Given a non-empty array of integers, return the ***k\*** most frequent elements.

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]
```

**Note:**

- You may assume *k* is always valid, 1 ≤ *k* ≤ number of unique elements.
- Your algorithm's time complexity **must be** better than O(*n* log *n*), where *n* is the array's size.
- It's guaranteed that the answer is unique, in other words the set of the top k frequent elements is unique.
- You can return the answer in any order.



### Algorithm

* use a dictionary to keep the occurrence of each item

* sort the dictionary by the value in descending order

* keep the first k items' key and return the answer

* Complexity:

  * Time: worst case O(NlogN) for sorting

  * space: O(N)

    

### Code

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        dic = collections.Counter(nums)
        ans = [k for k, v in sorted(dic.items(), key=lambda item: item[1], reverse=True)]
        return ans[:k]
```

