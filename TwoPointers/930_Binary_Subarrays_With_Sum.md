# 930. Binary Subarrays With Sum

2020/06/18 ZTH

### Problem Description

In an array `A` of `0`s and `1`s, how many **non-empty** subarrays have sum `S`?

**Example 1:**

```
Input: A = [1,0,1,0,1], S = 2
Output: 4
Explanation: 
The 4 subarrays are bolded below:
[1,0,1,0,1]
[1,0,1,0,1]
[1,0,1,0,1]
[1,0,1,0,1]
```

**Note:**

1. `A.length <= 30000`
2. `0 <= S <= A.length`
3. `A[i]` is either `0` or `1`.



### Algorithm

* We record the prefix sum of each position. And to find non-empty subarray with sum equals S, we could simply check for each prefix sum e whether e-S also exists.

  * ```
    e.g. input list 1, 0, 0, 1, 1, 0, 1, 1 
         prefix sum 1, 1, 1, 2, 3, 3, 4, 5
         S = 2:     (1,3) ==> [1] & [1,0,0,1,1] ==> [0,0,1,1] 
         									==> [1] & [1,0,0,1,1,0] ==> [0,0,1,1,0]
         						(2,4) ==> [1,0,0,1] & [1,0,0,1,1,0,1] ==> [1,0,1]
         						(3,5) ==> [1,0,0,1,1] & [1,0,0,1,1,0,1,1] ==> [0,1,1]
         						      ==> [1,0,0,1,1,0] & [1,0,0,1,1,0,1,1] ==> [1,1]
    ```

* Thus, after computing all the prefix sum, we maintain a dictionary to store the count of each prefix sum. While process each value e, if we could find e-S in the dictionary, simply add dic[e-S] to answer and update dic[e] for further calculation

* Complexity Analysis

  * Time: O(N)
  * Space: O(N)



### Code

```python
class Solution:
    def numSubarraysWithSum(self, A: List[int], S: int) -> int:
        if not A: return 0
        for i in range(1,len(A)):
            A[i] += A[i-1]
        dic, ans = {0:1}, 0
        for e in A:
            if e - S in dic: ans += dic[e-S]
            if e not in dic: dic[e] = 1
            else: dic[e] += 1
        return ans
```

