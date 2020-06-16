# 1004. Max Consecutive Ones III

2020/06/16 ZTH

### Problem Description

Given an array `A` of 0s and 1s, we may change up to `K` values from 0 to 1.

Return the length of the longest (contiguous) subarray that contains only 1s. 

 

**Example 1:**

```
Input: A = [1,1,1,0,0,0,1,1,1,1,0], K = 2
Output: 6
Explanation: 
[1,1,1,0,0,1,1,1,1,1,1]
Bolded numbers were flipped from 0 to 1.  The longest subarray is underlined.
```

**Example 2:**

```
Input: A = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], K = 3
Output: 10
Explanation: 
[0,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1]
Bolded numbers were flipped from 0 to 1.  The longest subarray is underlined.
```

 

**Note:**

1. `1 <= A.length <= 20000`
2. `0 <= K <= A.length`
3. `A[i]` is `0` or `1` 



### Algorithm

* Use a sliding window, which contains the continuous subarray with at most K 0s inside

* To get the maximum length, we can simply consider each time the sliding window contains K 0s as long as the array has at least K 0s, which would result in longest length.

* The key point is how to move the sliding window

  * Once we get a sliding window with K 0s inside, the next element to the right must be 0 (if has element), otherwise we could add 1 to our sliding window for a longer subarray

  * For the next possible answer, we could simply move the sliding window to the 1st 0's right element, end with the additional 0 and continue move the end if follows 1s

    * ```
      e.g. 1010111101011 ... K = 3
      current sliding window 1010111101
      next sliding window    10111101011... until find next 0
      ```

* Complexity Analysis

  * Time: O(N), scan the list once
  * Space: O(1) 



### Code

```python
class Solution:
    def longestOnes(self, A: List[int], K: int) -> int:
        left, right, ans, count = 0, 0, 0, 0
        while right < len(A):
            if A[right] == 0: count += 1
            if count > K:
                ans = max(ans, right - left)
                while left < len(A) and A[left] == 1: left += 1
                count -= 1
                left += 1
            right += 1
        if count <= K: ans = max(ans, right - left)
        return ans
            
```

