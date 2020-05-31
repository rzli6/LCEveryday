# 525. Contiguous Array

2020/05/31 ZTH

### Problem Description

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

**Example 1:**

```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```

**Example 2:**

```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```



### Algorithm

* use a variable count to keep # difference between 1s and 0s seen so far. see 0, decrease count by 1; see 1, increase count by 1

  ```
  e.g. input =     [0,1, 0, 0, 1,1]
  		 count = [0, -1,0,-1,-2,-1,0]
  		 index = [-1, 0,1, 2, 3, 4,5]
  		 once count at two position i,j are the same ==> the subarray i+1, ... j or i, ... j-1 has the same # 0s and 1s
  ```

* scan the input list once and use a dictionary to store these counts for each position

  ```
  dic = {0: [-1, 1, 5], -1: [0, 2, 4], -2: [3]}
  ```

* each time we update the ans to maintain the largest length of continous subarrray

* Complexity Analysis

  * Time: O(n) for one scan
  * Space: O(n)



### Code

```python
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        dic, ans, count = {0:[-1]}, 0, 0
        for i in range(len(nums)):
            if nums[i] == 1: count += 1
            else: count -= 1
            if count not in dic: dic[count] = [i]
            else: ans = max(ans, i - dic[count][0])
        return ans
        
```





