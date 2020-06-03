# 300. Longest Increasing Subsequence

2020/06/02 ZTH

### Problem Description

Given an unsorted array of integers, find the length of longest increasing subsequence.

**Example:**

```
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

**Note:**

- There may be more than one LIS combination, it is only necessary for you to return the length.
- Your algorithm should run in O(*n2*) complexity.

**Follow up:** Could you improve it to O(*n* log *n*) time complexity?



### Algorithm

* The length of longest increasing subsequence of each position of input nums is only related to previous ones (independent of later elements), thus we make use of previous results.

* We use a dp list variable to store the longest length of within each position

* For each position of input nums, there are two situations

  ```
  dp[i] = max(dp[j]) + 1 for 0 <= j < i once nums[i] > nums[j]
  dp[i] = 1 if nums[i] > nums[j] for all 0 <= j < i
  ```

* Calculate dp[i] for all i and keep the largest value which is the result

* Complexity Analysis

  * Time: O(N^2)
  * Space: O(N)



### Code

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if not nums: return 0
        dp, ans = [1], 1
        for i in range(1,len(nums)):
            current = 1
            for j in range(i):
                 if nums[i] > nums[j]: current = max(current, dp[j]+1)
            ans = max(ans, current)
            dp.append(current)
        return ans

```

