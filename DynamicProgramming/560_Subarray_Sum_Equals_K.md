# 560. Subarray Sum Equals K

2020/06/03 ZTH

### Problem Description

Given an array of integers and an integer **k**, you need to find the total number of continuous subarrays whose sum equals to **k**.

**Example 1:**

```
Input:nums = [1,1,1], k = 2
Output: 2
```

 

**Constraints:**

- The length of the array is in range [1, 20,000].
- The range of numbers in the array is [-1000, 1000] and the range of the integer **k** is [-1e7, 1e7].



### Algorithm

* To get subarrary with sum equals k, we utilize the following idea

  ```
  sum[i+1,j] = k ==> sum[0,j] - sum[0,i] = k
  ```

* Record subarray sum from 0 to each position in nums

  ```
  e.g. nums =   [1,1,1]
  		 sum  = [0,1,2,3]
  ```

* Use a dictionary to store these sum and # occurrences

  ```
  e.g. nums =   [1,1,1]
  		 sum  = [0,1,2,3]
  		 dic  = {0:1, 1:1, 2:1, 3:1}
  ```

* Each time we process a sum value, check whether sum - k exists in dictionary

  * if yes, ans is added by the occurrence of sum - k

* Complexity Analysis

  * Time: O(N) time, scan the input once
  * Space: O(N) for dictionary in worst case



### Code

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        dic, count, add = {0:1}, 0, 0
        for e in nums:
            # compute sum end at each position
            add += e
            # check whether add-k exists in dic
            if add - k in dic: count += dic[add-k]
            # update dic[add] value
            if add not in dic: dic[add] = 1
            else: dic[add] += 1
        return count
```

