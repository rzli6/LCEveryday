# 55. Jump Game

2020/06/25 ZTH

### Problem Description

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

**Example 1:**

```
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

**Constraints:**

- `1 <= nums.length <= 3 * 10^4`
- `0 <= nums[i][j] <= 10^5`



### Algorithm

Way1: Dynamic Programming (Time Limit Exceeded)

* Start from 2nd last element to check whether it could reach the last element and store the status (True, False), later use these value to update left elements
* For each element, we have 2 situations
  * Itself could reach the last element directly: nums[i] + i >= len(nums) - 1
  * It need to reach elements and later reach the last, need to check whether could reach an element with True status 
* Complexity Analysis
  * Time: O(n^2)
  * Space: O(n)

Way2: Greedy

* The key point is that we record the index of element we need to reach. Initially it was simply the last element of the list. Then it becomes the index of element which could reach previous last.
* We need to realize that if we could not reach i, there is no way for us to reach j for any j > i. 
* Complexity Analysis
  * Time: O(n)
  * Space: O(1)



### Code

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        # # Time Limit Exceeded: O(n^2) time, O(n) space
        # if len(nums) == 1: return True
        # dp = [False] * (len(nums) - 1)
        # for i in range(len(nums) - 2, -1, -1):
        #     if nums[i] >= len(nums) - i - 1: dp[i] = True
        #     else:
        #         maxjump = min(nums[i] + i, len(nums) - 2)
        #         for j in range(i+1, maxjump + 1):
        #                 if dp[j] == True:
        #                     dp[i] = True
        #                     break
        # return dp[0]
        last = len(nums) - 1
        for i in range(len(nums)-2, -1, -1):
            if i + nums[i] >= last: last = i
        return last == 0
```

